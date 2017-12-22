templates:
  private_rss:
    accept_all: yes
    download: /home/philbuckley/Documents/RSS/

tasks: 
  TheSite:
    verify_ssl_certificates: no
    rss: 
      url: https://wigornot.com/f/torrentrss.php?passkey=c0d41831b09b38dcb1d791437a33adc6
      all_entries: yes
    preset: private_rss