# From_Telegram
Parse and filter any message that arrives to a telegram bot!

## Preparations
* Create a bot & obtain a token for it (see https://core.telegram.org/bots#6-botfather).
* For direct messages (not to a group), start a conversation with the bot and click `START` in the Telegram app.
* For group messages, add the bot to the desired group and send a start message to the bot: `/start` (mind the
  leading `/`).
## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|token|text|Bot token. **Required**
|only_new|boolean|Only new messages are returned (Default: `yes`)
|whitelist|text|List of allowed type. Can be `username`, `group` or `fullname`. See config example for details. **Note:** Values here are case-sensitive
|entry|text|List of entry fields to be captured
  

## Config

```
  from_telegram:
    token: <bot_token>
    only_new: <yes|no>
    types:
      - <private|group>
    whitelist:
      <username|fullname|group>: <value_to_filter>
    entry:
      <field>: <regexp_to_match_value>
```

## Example
The user asks for a download, and the system adds that movie to a movie list. Then the user asks to run a task do download that movie, and the system will run a task that calls the download movie task.

```
tasks: 

  #Task To add a Movie to the Queue
  Telegram_Add_Movie:
    disable:
      - remember_rejected
      - seen
      - retry_failed
      - seen_info_hash

    imdb_lookup: yes
    
    from_telegram:
      token: "MY_TELEGRAM_BOT_TOKEN"
      only_new: yes
      types:
        - "private"
        - "group"
      whitelist:
        username: MY_USER_NAME
      entry:
        title: download (?:movie )?(.*)

      require_field:
        - imdb_name
        - imdb_id

    accept_all: yes

    list_add: 
      - movie_list: download_movie

    notify:
      entries:
        message: |+
          Ok, i'll download {{imdb_name}}
          [Image]({{(tvdb_posters|d|first )|d(imdb_photo)|d|replace("_", "%5F")}})
        via:
          - telegram:
              bot_token: "{? telegram.token ?}"
              parse_mode: markdown
              recipients: "{? telegram.from ?}"

  #Task to Run Downloads (Last we can clean the update)
  Telegram_Run_Task:
    disable:
      - remember_rejected
      - seen
      - retry_failed
      - seen_info_hash
    
    from_telegram:
      token: "MY_TELEGRAM_BOT_TOKEN"
      only_new: yes
      types:
        - "private"
        - "group"
      whitelist:
        username: MY_USER_NAME
      entry:
        title: ^([d|D]ownload [m|M]ovies)$

    accept_all: yes

    run_task:
      when: accepted
      task: Download_Movies

    notify:
      task:
        message: |+
          Download Task Started
        via:
          - telegram:
              bot_token: "MY_TELEGRAM_BOT_TOKEN"
              parse_mode: markdown
              recipients: 
                username: MY_USER_NAME


  Download_Movies:
    discover:
      interval: 1 minute
      what:
        - movie_list: download_movie
      from:
        - flexget_archive: [teste]
```

![image](https://user-images.githubusercontent.com/11949987/108549413-0ca2b880-72e5-11eb-8bba-6ff4c8e46c8f.png)
