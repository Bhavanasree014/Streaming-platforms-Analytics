# Streaming-platforms-Analytics
📊 Project Title: Streaming Platform Analytics
🎯 Objective:
The primary goal of this project is to analyze user behavior, content performance, and overall platform trends on a video streaming service. This includes tracking viewing patterns, subscription engagement, device usage, video session completion, and user satisfaction through ratings.

🧱 Database Overview:
The project uses a relational MySQL database consisting of 8 interconnected tables:

1.	users – Contains demographic and registration data of platform users.
2.	genres – Catalogs all available video genres (e.g., Drama, Comedy, Action).
3.	videos – Stores metadata for all uploaded video content.
4.	watch_history – Logs when users watched specific videos and for how long.
5.	ratings – Collects user-submitted ratings (1 to 5 stars) for videos.
6.	subscriptions – Tracks users’ subscription plans, statuses, and billing cycles.
7.	devices – Lists device types and operating systems used for streaming.
8.	video_sessions – Provides session-level data including video start/end time and completion flag.

🔍 Key Features:
	Identify high-performing videos by genre, rating, and completion rate.
	Analyze user behavior by age, gender, and device usage.
	Track subscription trends: active vs expired, plan types.
	Evaluate content engagement through watch duration and rewatch frequency.
	Detect peak streaming hours and days.

🧠 Sample Analyses:
🔍 1. Mo st Watched Genres by View Count
📺 2. Top 5 Most Watched Videos ?
🕒 3. Average Watch Time per Video ?
⭐ 4. Average Rating by Genre ?
📱 5. Most Common Device Types Used ?
🔄 6. User Retention Rate  ? (Monthly Signups vs Active Subs)
🧑🤝🧑 7. Gender-Based Genre Preferences ?
👥 8. Active Users per Subscription Plan ?
🌍 9. Most Watched Time of Day ?
🔁 10. Users with Repeat Views on Same Video ?

1. Finalized Table List (8 Tables)

1. users – Info about users
2. videos – Metadata of videos
3. genres – Video genre types
4. watch_history – What users watched and when
5. ratings – User ratings for videos
6. subscriptions – User subscription plans
7. devices – Devices used for streaming
8. video_sessions – Detailed video session logs

---

2. MySQL Table Schemas

1. users

CREATE TABLE users (
    user_id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50),
    email VARCHAR(100),
    signup_date DATE,
    gender ENUM('Male', 'Female', 'Other'),
    age INT
);

2. genres

CREATE TABLE genres (
    genre_id INT PRIMARY KEY AUTO_INCREMENT,
    genre_name VARCHAR(50)
);

3. videos

CREATE TABLE videos (
    video_id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(200),
    genre_id INT,
    duration_minutes INT,
    release_date DATE,
    FOREIGN KEY (genre_id) REFERENCES genres(genre_id)
);

4. watch_history

CREATE TABLE watch_history (
    watch_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    video_id INT,
    watch_date DATETIME,
    watch_duration_minutes INT,
    FOREIGN KEY (user_id) REFERENCES users(user_id),
    FOREIGN KEY (video_id) REFERENCES videos(video_id)
);

5. ratings

CREATE TABLE ratings (
    rating_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    video_id INT,
    rating INT CHECK (rating BETWEEN 1 AND 5),
    rating_date DATE,
    FOREIGN KEY (user_id) REFERENCES users(user_id),
    FOREIGN KEY (video_id) REFERENCES videos(video_id)
);

6. subscriptions

CREATE TABLE subscriptions (
    sub_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    start_date DATE,
    end_date DATE,
    plan_type ENUM('basic', 'standard', 'premium'),
    status ENUM('active', 'expired'),
    FOREIGN KEY (user_id) REFERENCES users(user_id)
);

7. devices

CREATE TABLE devices (
    device_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    device_type ENUM('mobile', 'tablet', 'desktop', 'smart_tv'),
    os VARCHAR(50),
    FOREIGN KEY (user_id) REFERENCES users(user_id)
);

8. video_sessions

CREATE TABLE video_sessions (
    session_id INT PRIMARY KEY AUTO_INCREMENT,
    user_id INT,
    video_id INT,
    start_time DATETIME,
    end_time DATETIME,
    completed BOOLEAN,
    FOREIGN KEY (user_id) REFERENCES users(user_id),
    FOREIGN KEY (video_id) REFERENCES videos(video_id)
);
