# Here are some guides
#
# https://ymgblog.com/2018/04/30/396/
# https://npchk.info/linux-flexget-rss/
# https://linkthis.me/2018/02/15/the-note-of-using-flexget/
#
# https://github.com/Aniverse/WiKi/blob/master/Flexget.md
# https://github.com/Aniverse/WiKi/blob/master/How.to.use.RSS.md#flexget-rss
#
# For more usages, check the offical site: https://flexget.com

templates:
  freespace:
    free_space:
      path: /home/eeqiulovept
      space: 10240【检查磁盘空间如果只有10G了就停止种子RSS自动化下载】
  qb:
    qbittorrent:
      path: /home/eeqiulovept/qbittorrent/download/
      host: localhost
      port: 2017
      username: eeqiulovept
      password: ptisverygood
  size:
    content_size:
      min: 1000【筛选文件大于1000M的种子】
      max: 51200【筛选文件小于50G的种子】
      strict: no
tasks:
  mt:
    rss: PT站RSS订阅地址
    accept_all: yes
    content_size:
      min: 1000【筛选文件大于1000M的种子】
      max: 51200【筛选文件小于50G的种子】
      strict: no
    template: tr
    clean_transmission:【自动删除种子】
      host: localhost
      port: 9099
      username: eeqiulovept
      password: ptisverygood
      finished_for: 48 hours【种子下载完成2天后删除】
      min_ratio: 5【种子分享率达到5以后，删除该种子】
      delete_files: Yes【删除种子的同时，删除下载的文件】
      enabled: Yes【启用自动删除种子插件】
web_server:
  port: 6566
  web_ui: yes