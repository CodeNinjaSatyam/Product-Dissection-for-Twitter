# Product Dissection for Twitter

## Introduction

Twitter, founded in 2006 by Jack Dorsey, Noah Glass, and Biz Stone, has revolutionized real-time communication and information sharing. With its character-limited posts (tweets), Twitter provides a platform for public discourse, news sharing, and user engagement on a global scale. This project dissects Twitter's product design and explores how its features address real-world challenges, offering practical solutions for accessing information quickly, engaging in meaningful conversations, amplifying content, and navigating through vast amounts of content efficiently.


## Top Features of Twitter
User: Contains user information. Each user can have multiple tweets, likes, retweets, followers, followees, and notifications.
Tweet: Represents tweets posted by users. Tweets can be replies to other tweets, indicated by the InReplyToTweetID.
Follow: Represents the relationship between followers and followees.
Like: Represents likes on tweets.
Retweet: Represents retweets of tweets.
DirectMessage: Represents private messages between users.
Notification: Represents notifications for various activities.
Hashtag: Represents hashtags used in tweets.
TweetHashtag: Represents the many-to-many relationship between tweets and hashtags.

## ERD Diagram

```plaintext
+-----------------+     +------------------+     +------------------+
|     User        |     |       Tweet      |     |     Hashtag      |
+-----------------+     +------------------+     +------------------+
| UserID (PK)     | 1   | TweetID (PK)     | N   | HashtagID (PK)   |
| Username        |-----| UserID (FK)      |-----| Tag (Unique)     |
| Password        |     | Content          |     +------------------+
| Email           |     | CreatedAt        |
| Name            |     | InReplyToTweetID (FK)  +------------------+
| Bio             |     +------------------+     |  TweetHashtag    |
| ProfilePicture  |                               +------------------+
| HeaderImage     |                               | TweetID (FK)     |
| CreatedAt       |                               | HashtagID (FK)   |
+-----------------+                               +------------------+
         | 1:N                                        |     |
         |                                             |     |
         v N                                           v N   v N
+-----------------+     +------------------+     +------------------+
|     Follow      |     |      Like        |     |    Retweet       |
+-----------------+     +------------------+     +------------------+
| FollowerID (FK) |     | LikeID (PK)      |     | RetweetID (PK)   |
| FolloweeID (FK) |-----| UserID (FK)      |-----| UserID (FK)      |
| FollowedAt      |     | TweetID (FK)     |     | TweetID (FK)     |
+-----------------+     | LikedAt          |     | RetweetedAt      |
                        +------------------+     +------------------+

         | 1:N
         v
+-----------------+
| DirectMessage   |
+-----------------+
| DMID (PK)       |
| SenderID (FK)   |
| ReceiverID (FK) |
| Content         |
| SentAt          |
+-----------------+

         | 1:N
         v
+-----------------+
|  Notification   |
+-----------------+
| NotificationID  |
| UserID (FK)     |
| Type            |
| RelatedEntityID |
| CreatedAt       |
+-----------------+
