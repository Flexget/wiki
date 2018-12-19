```
######## Secrets 참고 #########
variables: secrets.yml
######## scedules 설정 ########
schedules:
  # Download Tasks
  - tasks: ['download_*']
    interval:
      hours: 2  # weeks, days, hours, minutes
  - tasks: ['move_*']
    interval:
      hours: 1
######## templates 설정 ########
templates:
# Transmission 전송용 설정
  anchors:
    _transmission-settings: &transmission-settings
      host: 
      port: 
      username: 
      password: 

# Global Settings (항상 적용 되는 세팅, 적용안하려면 template: no_global)
  global:
    no_entries_ok: yes
    pathscrub: windows            # 파일 이름을 윈도우 형식으로 설정 (windows가 가장 엄격)
    free_space:
      path: "/{? folder.save_path ?}"  # secrets.yml 에서 설정한 다운로드 폴더가 있는 Root 폴더
      space: 5000                 # 5G 여유공간이 있어야 다운로드 진행

    regexp:
      reject:
        - (s|d)ub(s|bed)?\b: {from: title}    # subbed(영상 자체 자막), dubbed(더빙), etc 제외
        - \b3-?D\b: {from: title}             # 3D 제외
        - \btrailer\b: {from: title}          # 트레일러 제외
        - \bWEBSCR\b: {from: title}           # WEBSCR 제외 (화질구지)
        - \bTS\b: {from: title}               # TS, CAM 버전 제외 (화질구지)
        - \bCam\b: {from: title}

    manipulate:
      - title:
          replace:
          # JTBC, tvn, Olive, Mnet, 채널A 등 제거 (ex. [JTBC] 아는 형님 -> 아는 형님)
            regexp: '^\[[^\]]*\][^a-z0-9]'
            format: ''
    
    # 토렌트 설정
#    torrent_alive:
#      min_seeds: 3             # 필요한 최소 시드 수
#      reject_for: 15 minutes   # 15분 후에 다시 체크

    # 콘텐츠 필터 설정
    content_filter:
      require:  # 허용 확장자
        - '*.mkv'
        - '*.mp4'
      require_mainfile: yes       # 파일이 여러개 있는 경우, mainfile 체크 (단일파일은 상관X)
    magnets: no                 # 콘텐츠 필터가 적용되도록 마그넷(Magnet) 끄기

######## RSS 주소 설정 ########
# Korea ENT template
  kent_template:
    include: 
      - input/kent.yml
      - want/kent.yml
    verify_ssl_certificates: no
  # 콘텐츠 사이즈 설정
    content_size:
      min: 300  # 300MB 이상
      max: 5000 # 5G 이하
    series:
      settings:
        KENT:
          identified_by: ep
          ep_regexp: e(\d+)
          quality: 720p !1080p !360p

# Korea Drama template
  kdrama_template:
    include: 
      - input/kdrama.yml
      - want/kdrama.yml
    verify_ssl_certificates: no
  # 콘텐츠 사이즈 설정
    content_size:
      min: 300  # 300MB 이상
      max: 5000 # 5G 이하
    series:
      settings:
        KDRAMA:
          identified_by: ep
          ep_regexp: e(\d+)
          quality: 720p 1080p !360p

# 저장 폴더 및 파일이름 변경 설정
  transmission-kent:
    transmission:
      <<: *transmission-settings
      ratio: 0
      main_file_only: yes
      rename_like_files: no
      #content_filename: "{{tvdb_series_name|default(series_name)|pathscrub}} - {{tvdb_ep_id|default(series_id)}}{% if tvdb_ep_name|default(False) %} - {{tvdb_ep_name|pathscrub}}{% endif %}{% if quality|default(False) %} - [{{quality}}]{% endif %}"
      path: "/{? folder.down_path ?}{? folder.downkent ?}/"

  transmission-kdrama:
    transmission:
      <<: *transmission-settings
      ratio: 0
      main_file_only: yes
      rename_like_files: no
      #content_filename: "{{tvdb_series_name|default(series_name)|pathscrub}} - {{tvdb_ep_id|default(series_id)}}{% if tvdb_ep_name|default(False) %} - {{tvdb_ep_name|pathscrub}}{% endif %}{% if quality|default(False) %} - [{{quality}}]{% endif %}"
      path: "/{? folder.down_path ?}{? folder.downkdrama ?}{{tmdb_name|default(series_name)|pathscrub}}/"

# Pushbullet 설정
  pushbullet:
    notify:
      entries:
        title: "{{title}} 다운로드 시작"
        via:
          - pushbullet:
              api_key: "{? pushbullet.api ?}"

  disable-seen-retry:
    disable:
      - seen
      - seen_info_hash
      - retry_failed
      
  series-metainfo:
    metainfo_series: yes
    #tmdb_lookup: yes
    thetvdb_lookup: yes

  series-guessit:
    parsing:
      series: guessit

  movies-metainfo:
    metainfo_movie: yes
    tmdb_lookup: yes
    parsing:
      movie: guessit
################################

tasks:
  download_kent_rss:
    priority: 10
    template:
      - disable-seen-retry
      - kent_template
      - transmission-kent
      - pushbullet

  download_kdrama_rss:
    priority: 10
    template:
      - disable-seen-retry
      - kdrama_template
      - transmission-kdrama


############ 이동 ############
  move_kent:
    priority: 50
    filesystem:
      path: "/{? folder.down_path ?}{? folder.downkent ?}"
      recursive: yes
      retrieve: files
      regexp: '.*\.(avi|mkv|mp4)$'
    accept_all: yes
    move:
      to: "/{? folder.save_path ?}{? folder.kent ?}"
    exec:
      on_exit:
        phase: find "/{? folder.down_path ?}{? folder.downkent ?}"* -type d -empty -delete

  move_kdrama:
    priority: 51
    filesystem:
      path: "/{? folder.down_path ?}{? folder.downkdrama ?}"
      recursive: yes
      retrieve: files
      regexp: '.*\.(avi|mkv|mp4)$'
    accept_all: yes
    move:
      to: "/{? folder.save_path ?}{? folder.kdrama ?}{{tmdb_name|default(series_name)|pathscrub}}/"
    exec:
      on_exit:
        phase: find "/{? folder.down_path ?}{? folder.downkdrama ?}"* -type d -empty -delete
