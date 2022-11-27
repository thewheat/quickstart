# Telegram Bots

- https://core.telegram.org/bots
- https://core.telegram.org/bots/api

## Create Bot

- https://t.me/BotFather
- From here you can modify settings and get token needed to make API calls


## Making Telegram API Requests

- Send requests to: `https://api.telegram.org/bot<token>/METHOD_NAME`
              <token>`:                               is the unique token for the bo   : API action to tak   Where, passing parameters via
    - URL query string
    - application/x-www-form-urlencoded
    - application/json (except for uploading files)
    - multipart/form-data (use to upload files)
- Response: a JSON object with the following fields
               ok` b                              oolean (`true`/`false`) indicating if the query was successfu    object) with resulting data from quer    string) with a human-readable description of the result / erro    integer   All in the Bot API are case-insensitive.
- All queries must be made using UTF-8.

## Receiving Messages / Getting Updates

- 2 methods
   - Polling via `getUpdates` https://core.telegram.org/bots/api#getupdates
   - Webhooks https://core.telegram.org/bots/api#setwebhook
- Incoming updates are stored on the server until the bot receives them either way, but they will not be kept longer than 24 hours.
- Data will be JSON-serialized `Update` object https://core.telegram.org/bots/api#update

### Webhooks

- Each message is sent to webhook URL to process and respond
https://core.telegram.org/bots/webhooks#how-do-i-set-a-webhook-for-either-type

#### Set Webhook
```
TOKEN=""
WEBHOOK_ENDPOINT="https://yourdomain.com/telegram_webhook/"
curl -F "url=$WEBHOOK_ENDPOINT" https://api.telegram.org/bot$TOKEN/setWebhook
```

#### Get Current Webhook
```
TOKEN=""
curl https://api.telegram.org/bot$TOKEN/getWebhookInfo
```

## Sending Messages

- You interact with a User in a Chat by sending Messages
  - https://core.telegram.org/bots/api#user
  - https://core.telegram.org/bots/api#chat
  - https://core.telegram.org/bots/api#message

- To send Messages you will need the chat_id (if responding to a message the chat_id will be sent as incmoing message)


### User 
https://core.telegram.org/bots/api#user

```
                      Field   Type      Description
-----------------------------------------------------------------------------------------------------------------------------------------------------
                         id   Integer   Unique identifier for this user or bot. This number may have more than 32 significant bits and some programming languages may have difficulty/silent defects in interpreting it. But it has at most 52 significant bits, so a 64-bit integer or double-precision float type are safe for storing this identifier.
                     is_bot   Boolean   True, if this user is a bot
                 first_name   String    User's or bot's first name
                  last_name   String    Optional. User's or bot's last name
                   username   String    Optional. User's or bot's username
              language_code   String    Optional. IETF language tag of the user's language
                 is_premium   True      Optional. True, if this user is a Telegram Premium user
   added_to_attachment_menu   True      Optional. True, if this user added the bot to the attachment menu
            can_join_groups   Boolean   Optional. True, if the bot can be invited to groups. Returned only in getMe.
can_read_all_group_messages   Boolean   Optional. True, if privacy mode is disabled for the bot. Returned only in getMe.
    supports_inline_queries   Boolean   Optional. True, if the bot supports inline queries. Returned only in getMe.
```

### Chat
https://core.telegram.org/bots/api#chat
```
                                  Field   Type              Description
-----------------------------------------------------------------------------------------------------------------------------------------------------
                                     id   Integer           Unique identifier for this chat. This number may have more than 32 significant bits and some programming languages may have difficulty/silent defects in interpreting it. But it has at most 52 significant bits, so a signed 64-bit integer or double-precision float type are safe for storing this identifier.
                                   type   String            Type of chat, can be either “private”, “group”, “supergroup” or “channel”
                                  title   String            Optional. Title, for supergroups, channels and group chats
                               username   String            Optional. Username, for private chats, supergroups and channels if available
                             first_name   String            Optional. First name of the other party in a private chat
                              last_name   String            Optional. Last name of the other party in a private chat
                               is_forum   True              Optional. True, if the supergroup chat is a forum (has topics enabled)
                                  photo   ChatPhoto         Optional. Chat photo. Returned only in getChat.
                       active_usernames   String            Optional. If non-empty, the list of all active chat usernames; for private chats, supergroups and channels. Returned only in getChat.
           emoji_status_custom_emoji_id   String            Optional. Custom emoji identifier of emoji status of the other party in a private chat. Returned only in getChat.
                                    bio   String            Optional. Bio of the other party in a private chat. Returned only in getChat.
                   has_private_forwards   True              Optional. True, if privacy settings of the other party in the private chat allows to use tg://user?id=<user_id> links only in chats with the user. Returned only in getChat.
has_restricted_voice_and_video_messages   True              Optional. True, if the privacy settings of the other party restrict sending voice and video note messages in the private chat. Returned only in getChat.
                  join_to_send_messages   True              Optional. True, if users need to join the supergroup before they can send messages. Returned only in getChat.
                        join_by_request   True              Optional. True, if all users directly joining the supergroup need to be approved by supergroup administrators. Returned only in getChat.
                            description   String            Optional. Description, for groups, supergroups and channel chats. Returned only in getChat.
                            invite_link   String            Optional. Primary invite link, for groups, supergroups and channel chats. Returned only in getChat.
                         pinned_message   Message           Optional. The most recent pinned message (by sending date). Returned only in getChat.
                            permissions   ChatPermissions   Optional. Default chat member permissions, for groups and supergroups. Returned only in getChat.
                        slow_mode_delay   Integer           Optional. For supergroups, the minimum allowed delay between consecutive messages sent by each unpriviledged user; in seconds. Returned only in getChat.
               message_auto_delete_time   Integer           Optional. The time after which all messages sent to the chat will be automatically deleted; in seconds. Returned only in getChat.
                  has_protected_content   True              Optional. True, if messages from the chat can't be forwarded to other chats. Returned only in getChat.
                       sticker_set_name   String            Optional. For supergroups, name of group sticker set. Returned only in getChat.
                    can_set_sticker_set   True              Optional. True, if the bot can change the group sticker set. Returned only in getChat.
                         linked_chat_id   Integer           Optional. Unique identifier for the linked chat, i.e. the discussion group identifier for a channel and vice versa; for supergroups and channel chats. This identifier may be greater than 32 bits and some programming languages may have difficulty/silent defects in interpreting it. But it is smaller than 52 bits, so a signed 64 bit integer or double-precision float type are safe for storing this identifier. Returned only in getChat.
                               location   ChatLocation      Optional. For supergroups, the location to which the supergroup is connected. Returned only in getChat.
```

### Message

https://core.telegram.org/bots/api#message

```
                            Field   Type                             Description
-----------------------------------------------------------------------------------------------------------------------------------------------------
                       message_id   Integer                          Unique message identifier inside this chat
                message_thread_id   Integer                          Optional. Unique identifier of a message thread to which the message belongs; for supergroups only
                             from   User                             Optional. Sender of the message; empty for messages sent to channels. For backward compatibility, the field contains a fake sender user in non-channel chats, if the message was sent on behalf of a chat.
                      sender_chat   Chat                             Optional. Sender of the message, sent on behalf of a chat. For example, the channel itself for channel posts, the supergroup itself for messages from anonymous group administrators, the linked channel for messages automatically forwarded to the discussion group. For backward compatibility, the field from contains a fake sender user in non-channel chats, if the message was sent on behalf of a chat.
                             date   Integer                          Date the message was sent in Unix time
                             chat   Chat                             Conversation the message belongs to
                     forward_from   User                             Optional. For forwarded messages, sender of the original message
                forward_from_chat   Chat                             Optional. For messages forwarded from channels or from anonymous administrators, information about the original sender chat
          forward_from_message_id   Integer                          Optional. For messages forwarded from channels, identifier of the original message in the channel
                forward_signature   String                           Optional. For forwarded messages that were originally sent in channels or by an anonymous chat administrator, signature of the message sender if present
              forward_sender_name   String                           Optional. Sender's name for messages forwarded from users who disallow adding a link to their account in forwarded messages
                     forward_date   Integer                          Optional. For forwarded messages, date the original message was sent in Unix time
                 is_topic_message   True                             Optional. True, if the message is sent to a forum topic
             is_automatic_forward   True                             Optional. True, if the message is a channel post that was automatically forwarded to the connected discussion group
                 reply_to_message   Message                          Optional. For replies, the original message. Note that the Message object in this field will not contain further reply_to_message fields even if it itself is a reply.
                          via_bot   User                             Optional. Bot through which the message was sent
                        edit_date   Integer                          Optional. Date the message was last edited in Unix time
            has_protected_content   True                             Optional. True, if the message can't be forwarded
                   media_group_id   String                           Optional. The unique identifier of a media message group this message belongs to
                 author_signature   String                           Optional. Signature of the post author for messages in channels, or the custom title of an anonymous group administrator
                             text   String                           Optional. For text messages, the actual UTF-8 text of the message
                         entities   Array of MessageEntity           Optional. For text messages, special entities like usernames, URLs, bot commands, etc. that appear in the text
                        animation   Animation                        Optional. Message is an animation, information about the animation. For backward compatibility, when this field is set, the document field will also be set
                            audio   Audio                            Optional. Message is an audio file, information about the file
                         document   Document                         Optional. Message is a general file, information about the file
                            photo   Array of PhotoSize               Optional. Message is a photo, available sizes of the photo
                          sticker   Sticker                          Optional. Message is a sticker, information about the sticker
                            video   Video                            Optional. Message is a video, information about the video
                       video_note   VideoNote                        Optional. Message is a video note, information about the video message
                            voice   Voice                            Optional. Message is a voice message, information about the file
                          caption   String                           Optional. Caption for the animation, audio, document, photo, video or voice
                 caption_entities   Array of MessageEntity           Optional. For messages with a caption, special entities like usernames, URLs, bot commands, etc. that appear in the caption
                          contact   Contact                          Optional. Message is a shared contact, information about the contact
                             dice   Dice                             Optional. Message is a dice with random value
                             game   Game                             Optional. Message is a game, information about the game. More about games »
                             poll   Poll                             Optional. Message is a native poll, information about the poll
                            venue   Venue                            Optional. Message is a venue, information about the venue. For backward compatibility, when this field is set, the location field will also be set
                         location   Location                         Optional. Message is a shared location, information about the location
                 new_chat_members   Array of User                    Optional. New members that were added to the group or supergroup and information about them (the bot itself may be one of these members)
                 left_chat_member   User                             Optional. A member was removed from the group, information about them (this member may be the bot itself)
                   new_chat_title   String                           Optional. A chat title was changed to this value
                   new_chat_photo   Array of PhotoSize               Optional. A chat photo was change to this value
                delete_chat_photo   True                             Optional. Service message: the chat photo was deleted
               group_chat_created   True                             Optional. Service message: the group has been created
          supergroup_chat_created   True                             Optional. Service message: the supergroup has been created. This field can't be received in a message coming through updates, because bot can't be a member of a supergroup when it is created. It can only be found in reply_to_message if someone replies to a very first message in a directly created supergroup.
             channel_chat_created   True                             Optional. Service message: the channel has been created. This field can't be received in a message coming through updates, because bot can't be a member of a channel when it is created. It can only be found in reply_to_message if someone replies to a very first message in a channel.
message_auto_delete_timer_changed   MessageAutoDeleteTimerChanged    Optional. Service message: auto-delete timer settings changed in the chat
               migrate_to_chat_id   Integer                          Optional. The group has been migrated to a supergroup with the specified identifier. This number may have more than 32 significant bits and some programming languages may have difficulty/silent defects in interpreting it. But it has at most 52 significant bits, so a signed 64-bit integer or double-precision float type are safe for storing this identifier.
             migrate_from_chat_id   Integer                          Optional. The supergroup has been migrated from a group with the specified identifier. This number may have more than 32 significant bits and some programming languages may have difficulty/silent defects in interpreting it. But it has at most 52 significant bits, so a signed 64-bit integer or double-precision float type are safe for storing this identifier.
                   pinned_message   Message                          Optional. Specified message was pinned. Note that the Message object in this field will not contain further reply_to_message fields even if it is itself a reply.
                          invoice   Invoice                          Optional. Message is an invoice for a payment, information about the invoice. More about payments »
               successful_payment   SuccessfulPayment                Optional. Message is a service message about a successful payment, information about the payment. More about payments »
                connected_website   String                           Optional. The domain name of the website on which the user has logged in. More about Telegram Login »
                    passport_data   PassportData                     Optional. Telegram Passport data
        proximity_alert_triggered   ProximityAlertTriggered          Optional. Service message. A user in the chat triggered another user's proximity alert while sharing Live Location.
              forum_topic_created   ForumTopicCreated                Optional. Service message: forum topic created
               forum_topic_closed   ForumTopicClosed                 Optional. Service message: forum topic closed
             forum_topic_reopened   ForumTopicReopened               Optional. Service message: forum topic reopened
             video_chat_scheduled   VideoChatScheduled               Optional. Service message: video chat scheduled
               video_chat_started   VideoChatStarted                 Optional. Service message: video chat started
                 video_chat_ended   VideoChatEnded                   Optional. Service message: video chat ended
  video_chat_participants_invited   VideoChatParticipantsInvited     Optional. Service message: new participants invited to a video chat
                     web_app_data   WebAppData                       Optional. Service message: data sent by a Web App
                     reply_markup   InlineKeyboardMarkup             Optional. Inline keyboard attached to the message. login_url buttons are represented as ordinary url button
```
### Send a text message / sendMessage

- Method name: `sendMessage`
- https://core.telegram.org/bots/api#sendmessage
- Send text message
- On success, the sent `Message` is returned

```
                  Parameter   Type                     Required   Description
------------------------------------------------------------------------------------------------------------------------------------------------------------------
                    chat_id   Integer or String             Yes   Unique identifier for the target chat or username of the target channel (in the format @channelusername)
                       text   String                        Yes   Text of the message to be sent, 1-4096 characters after entities parsing
          message_thread_id   Integer                  Optional   Unique identifier for the target message thread (topic) of the forum; for forum supergroups only
                 parse_mode   String                   Optional   Mode for parsing entities in the message text. See formatting options for more details.
                   entities   Array of MessageEntity   Optional   A JSON-serialized list of special entities that appear in message text, which can be specified instead of parse_mode
   disable_web_page_preview   Boolean                  Optional   Disables link previews for links in this message
       disable_notification   Boolean                  Optional   Sends the message silently. Users will receive a notification with no sound.
            protect_content   Boolean                  Optional   Protects the contents of the sent message from forwarding and saving
        reply_to_message_id   Integer                  Optional   If the message is a reply, ID of the original message
allow_sending_without_reply   Boolean                  Optional   Pass True if the message should be sent even if the specified replied-to message is not found
               reply_markup   InlineKeyboardMarkup     Optional   Additional interface options. A JSON-serialized object for an inline keyboard, custom reply keyboard, instructions to remove reply keyboard or to force a reply from the user.
                              or ReplyKeyboardMarkup 
                              or ReplyKeyboardRemove 
                              or ForceReply
```

### Send Photos / `sendPhoto` 

- Method name: `sendPhoto` https://core.telegram.org/bots/api#sendphoto
- Send photos
- On success, the sent `Message` is returned

```
                  Parameter   Type                     Required   Description
------------------------------------------------------------------------------------------------------------------------------------------------------------------
                    chat_id   Integer or String             Yes   Unique identifier for the target chat or username of the target channel (in the format @channelusername)
                      photo   InputFile or String           Yes   Photo to send. Pass a file_id as String to send a photo that exists on the Telegram servers (recommended), pass an HTTP URL as a String for Telegram to get a photo from the Internet, or upload a new photo using multipart/form-data. The photo must be at most 10 MB in size. The photo's width and height must not exceed 10000 in total. Width and height ratio must be at most 20. More information on Sending Files »
          message_thread_id   Integer                  Optional   Unique identifier for the target message thread (topic) of the forum; for forum supergroups only
                    caption   String                   Optional   Photo caption (may also be used when resending photos by file_id), 0-1024 characters after entities parsing
                 parse_mode   String                   Optional   Mode for parsing entities in the photo caption. See formatting options for more details.
           caption_entities   Array of MessageEntity   Optional   A JSON-serialized list of special entities that appear in the caption, which can be specified instead of parse_mode
       disable_notification   Boolean                  Optional   Sends the message silently. Users will receive a notification with no sound.
            protect_content   Boolean                  Optional   Protects the contents of the sent message from forwarding and saving
        reply_to_message_id   Integer                  Optional   If the message is a reply, ID of the original message
allow_sending_without_reply   Boolean                  Optional   Pass True if the message should be sent even if the specified replied-to message is not found
               reply_markup   InlineKeyboardMarkup     Optional   Additional interface options. A JSON-serialized object for an inline keyboard, custom reply keyboard, instructions to remove reply keyboard or to force a reply from the user. 
                              or ReplyKeyboardMarkup
                              or ReplyKeyboardRemove
                              or ForceReply
```

### Send status message while waiting for response / `sendChatAction`

- https://core.telegram.org/bots/api#sendchataction
- Send a status message while waiting for a response on the bot's side
- The status is set for 5 seconds or less (when a message arrives from your bot, Telegram clients clear its typing status)
- Returns True on success

```
Parameter                Type   Required   Description
----------------------------------------------------------------------------------------
  chat_id   Integer or String        Yes   Unique identifier for the target chat or username of the target channel (in the format @channelusername)
   action   String                   Yes   Type of action to broadcast. 
                                            `typing` for text messages
                                            `upload_photo` for photos
                                            `record_video` or `upload_video` for videos
                                            `record_voice` or `upload_voice` for voice notes
                                            `upload_document` for general files
                                            `choose_sticker` for stickers
                                            `find_location` for location data
                                            `record_video_note` or `upload_video_note` for video notes
```