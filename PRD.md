# DeenQuest - Product Requirements Document (PRD)

## 📋 Project Overview

**Project Name:** DeenQuest  
**Project Type:** Web Application (Laravel + MySQL)  
**Tagline:** Structured Islamic Learning Journey Platform  
**Core Functionality:** A gamified, day-by-day Islamic education platform where users track their learning progress from basics to scholarship level.  
**Target Users:** Muslims seeking structured Islamic education (ages 10+), parents teaching children, dawah initiatives.

---

## 🎯 Vision

Build a complete Laravel-based learning management system where users:
- Create accounts and track progress
- Learn day-by-day with interactive lessons
- Earn stars, badges, and achievements
- Compete with friends (optional)
- Access from any device

---

## 🎨 Color Palette & Theme

### Primary Colors

| Color Name | Hex Code | Usage |
|-----------|---------|-------|
| Primary | `#1a5f4a` | Headers, buttons, highlights |
| Primary Dark | `#0d3f32` | Footer, dark sections |
| Primary Light | `#2d8a6e` | Hover states, secondary elements |
| Secondary | `#2d8a6e` | Accent buttons, links |

### Accent Colors

| Color Name | Hex Code | Usage |
|-----------|---------|-------|
| Gold | `#e9c46a` | Stars, rewards, achievements |
| Gold Dark | `#d4a849` | Hover for gold elements |
| Accent Orange | `#f4a261` | CTAs, notifications |

### Background Colors

| Color Name | Hex Code | Usage |
|-----------|---------|-------|
| BG Grad Start | `#e8f5e9` | Page background top |
| BG Grad End | `#f0fdf4` | Page background bottom |
| Card White | `#ffffff` | Cards, content areas |
| Surface | `#f8faf9` | Alternate card bg |

### Text Colors

| Color Name | Hex Code | Usage |
|-----------|---------|-------|
| Text Main | `#1e293b` | Primary text |
| Text Muted | `#64748b` | Secondary text |
| Text Light | `#94a3b8` | Placeholder text |

### Status Colors

| Color Name | Hex Code | Usage |
|-----------|---------|-------|
| Success | `#22c55e` | Completed, correct |
| Warning | `#f59e0b` | In progress |
| Error | `#dc2626` | Wrong, urgent |
| Info | `#0ea5e9` | Information |

### CSS Variables (Ready to Copy)

```css
:root {
    /* Primary */
    --primary: #1a5f4a;
    --primary-dark: #0d3f32;
    --primary-light: #2d8a6e;
    --secondary: #2d8a6e;
    
    /* Accent */
    --accent: #e9c46a;
    --accent-dark: #d4a849;
    --accent-orange: #f4a261;
    
    /* Background */
    --bg-grad-start: #e8f5e9;
    --bg-grad-end: #f0fdf4;
    --white: #ffffff;
    --surface: #f8faf9;
    
    /* Text */
    --text-main: #1e293b;
    --text-muted: #64748b;
    --text-light: #94a3b8;
    
    /* Status */
    --success: #22c55e;
    --warning: #f59e0b;
    --error: #dc2626;
    --info: #0ea5e9;
}
```

---

## 🏗️ Technical Stack

| Component | Technology |
|-----------|-------------|
| Backend | Laravel 10+ |
| Database | MySQL 8.0+ |
| Frontend | Blade + Tailwind CSS |
| Authentication | Laravel Breeze / Jetstream |
| State Management | Laravel Session + DB |
| Hosting | Shared / VPS / Laravel Forge |

---

## 📊 Database Schema

### Users Table
```sql
CREATE TABLE users (
    id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    avatar VARCHAR(255) DEFAULT NULL,
    current_day INT UNSIGNED DEFAULT 1,
    current_phase INT UNSIGNED DEFAULT 1,
    total_stars INT UNSIGNED DEFAULT 0,
    streak_days INT UNSIGNED DEFAULT 0,
    last_active_date DATE DEFAULT NULL,
    role ENUM('student', 'admin') DEFAULT 'student',
    email_verified_at TIMESTAMP DEFAULT NULL,
    remember_token VARCHAR(100) DEFAULT NULL,
    created_at TIMESTAMP NULL,
    updated_at TIMESTAMP NULL
);
```

### Phases Table
```sql
CREATE TABLE phases (
    id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    name_en VARCHAR(255) NOT NULL,
    name_bn VARCHAR(255) NOT NULL,
    slug VARCHAR(100) UNIQUE NOT NULL,
    description_en TEXT,
    description_bn TEXT,
    day_start INT UNSIGNED NOT NULL,
    day_end INT UNSIGNED NOT NULL,
    icon VARCHAR(50) DEFAULT '📚',
    order_index INT UNSIGNED DEFAULT 0,
    created_at TIMESTAMP NULL,
    updated_at TIMESTAMP NULL
);
```

### Days Table
```sql
CREATE TABLE days (
    id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    phase_id INT UNSIGNED NOT NULL,
    day_number INT UNSIGNED NOT NULL,
    topic_en VARCHAR(255) NOT NULL,
    topic_bn VARCHAR(255) NOT NULL,
    summary_en TEXT,
    summary_bn TEXT,
    order_index INT UNSIGNED DEFAULT 0,
    created_at TIMESTAMP NULL,
    updated_at TIMESTAMP NULL,
    FOREIGN KEY (phase_id) REFERENCES phases(id) ON DELETE CASCADE
);
```

### Lessons Table
```sql
CREATE TABLE lessons (
    id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    day_id INT UNSIGNED NOT NULL,
    section_key VARCHAR(50) NOT NULL, -- 'knowledge', 'heart', 'memorization', 'practice', 'test', 'homework'
    title_en VARCHAR(255) NOT NULL,
    title_bn VARCHAR(255) NOT NULL,
    content_en TEXT,
    content_bn TEXT,
    order_index INT UNSIGNED DEFAULT 0,
    created_at TIMESTAMP NULL,
    updated_at TIMESTAMP NULL,
    FOREIGN KEY (day_id) REFERENCES days(id) ON DELETE CASCADE
);
```

### Duas/Memorization Table
```sql
CREATE TABLE memos (
    id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    day_id INT UNSIGNED NOT NULL,
    arabic_text TEXT NOT NULL,
    transliteration VARCHAR(255),
    meaning_en TEXT,
    meaning_bn TEXT,
    audio_url VARCHAR(500) DEFAULT NULL,
    video_url VARCHAR(500) DEFAULT NULL,
    order_index INT UNSIGNED DEFAULT 0,
    created_at TIMESTAMP NULL,
    updated_at TIMESTAMP NULL,
    FOREIGN KEY (day_id) REFERENCES days(id) ON DELETE CASCADE
);
```

### User Progress Table
```sql
CREATE TABLE user_progress (
    id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    user_id BIGINT UNSIGNED NOT NULL,
    day_id INT UNSIGNED NOT NULL,
    status ENUM('not_started', 'in_progress', 'completed') DEFAULT 'not_started',
    stars_earned INT UNSIGNED DEFAULT 0,
    quiz_score INT UNSIGNED DEFAULT 0,
    completed_at TIMESTAMP NULL,
    created_at TIMESTAMP NULL,
    updated_at TIMESTAMP NULL,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE,
    FOREIGN KEY (day_id) REFERENCES days(id) ON DELETE CASCADE,
    UNIQUE KEY unique_user_day (user_id, day_id)
);
```

### Achievements Table
```sql
CREATE TABLE achievements (
    id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    name_en VARCHAR(255) NOT NULL,
    name_bn VARCHAR(255) NOT NULL,
    description_en TEXT,
    description_bn TEXT,
    icon VARCHAR(50) DEFAULT '🏆',
    requirement_type VARCHAR(50), -- 'days_completed', 'stars_earned', 'streak', 'phase_completed'
    requirement_value INT UNSIGNED,
    stars_reward INT UNSIGNED DEFAULT 0,
    created_at TIMESTAMP NULL,
    updated_at TIMESTAMP NULL
);
```

### User Achievements Table
```sql
CREATE TABLE user_achievements (
    id BIGINT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    user_id BIGINT UNSIGNED NOT NULL,
    achievement_id INT UNSIGNED NOT NULL,
    earned_at TIMESTAMP NULL,
    created_at TIMESTAMP NULL,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE,
    FOREIGN KEY (achievement_id) REFERENCES achievements(id) ON DELETE CASCADE,
    UNIQUE KEY unique_user_achievement (user_id, achievement_id)
);
```

---

## 📱 Key Features

### Authentication
- [ ] User Registration (name, email, password)
- [ ] Login / Logout
- [ ] Password Reset
- [ ] Email Verification (optional)
- [ ] Profile Management (name, avatar)

### Dashboard
- [ ] Current day lesson CTA button
- [ ] Progress bar (days completed / 365)
- [ ] Current phase display
- [ ] Stars earned
- [ ] Streak counter
- [ ] Recent achievements

### Learning System
- [ ] Day-by-day lesson navigation
- [ ] Previous / Next day buttons
- [ ] Section-by-section content
- [ ] Audio player for Arabic/duas
- [ ] Video links where applicable
- [ ] Interactive quizzes
- [ ] Star rewards on quiz completion

### Gamification
- [ ] Star system (earn stars per quiz)
- [ ] Achievement badges
- [ ] Streak tracking (consecutive days)
- [ ] Phase completion badges

### Progress Tracking
- [ ] Mark day as complete
- [ ] Track quiz scores
- [ ] Save memorization progress
- [ ] Resume from last position

### Admin Panel
- [ ] CRUD for Phases
- [ ] CRUD for Days
- [ ] CRUD for Lessons
- [ ] CRUD for Duas/Memos
- [ ] View all user progress
- [ ] Manage achievements

---

## 📄 Page Structure

### Public Pages
| Route | Page | Description |
|-------|------|-------------|
| `/` | Home | Landing with phases overview |
| `/about` | About | Why this project |
| `/plan` | Plan | Full day-by-day list |

### Auth Pages
| Route | Page | Description |
|-------|------|-------------|
| `/login` | Login | User login form |
| `/register` | Register | User registration |
| `/forgot-password` | Forgot Password | Password reset |

### Protected Pages (Requires Login)
| Route | Page | Description |
|-------|------|-------------|
| `/dashboard` | Dashboard | Main progress view |
| `/learn/day/{id}` | Lesson | Interactive lesson |
| `/learn/day/{id}/complete` | Mark Complete | API endpoint |
| `/profile` | Profile | User settings |
| `/achievements` | Achievements | All badges earned |

### Admin Pages (Requires Admin Role)
| Route | Page | Description |
|-------|------|-------------|
| `/admin/phases` | Manage Phases | CRUD phases |
| `/admin/days` | Manage Days | CRUD days |
| `/admin/lessons` | Manage Lessons | CRUD lessons |
| `/admin/duas` | Manage Duas | CRUD memos |
| `/admin/users` | Manage Users | View all users |
| `/admin/achievements` | Manage Achievements | CRUD achievements |

---

## 🎮 User Flow

```
1. User visits site → sees home with phases
2. User clicks "Start Learning" → redirect to login/register
3. After login → redirect to dashboard
4. User clicks "Start Day 1" → goes to lesson page
5. User reads content, listens to audio, takes quiz
6. User clicks "Complete Day" → progress saved
7. Stars awarded → achievements check
8. Next day unlocked → user returns tomorrow
```

---

## 🧩 Milestones (MVP)

### Phase 1: Setup
- [ ] Laravel project init
- [ ] Database schema
- [ ] Authentication
- [ ] Theme applied

### Phase 2: Core Learning
- [ ] Home page
- [ ] Dashboard
- [ ] Day 1 lesson display
- [ ] Day navigation

### Phase 3: Interaction
- [ ] Quiz functionality
- [ ] Progress tracking
- [ ] Star system

### Phase 4: Gamification
- [ ] Achievements
- [ ] Streak tracking
- [ ] Profile page

### Phase 5: Admin
- [ ] Admin panels
- [ ] Content management

---

## 📦 Deliverables

1. **Laravel Project** - Full source code
2. **Database** - MySQL schema + seeders
3. **Theme** - Tailwind config with color palette
4. **Documentation** - This PRD
5. **API Endpoints** - For mobile app (future)

---

## 📅 Timeline Suggestion

| Week | Deliverable |
|------|--------------|
| Week 1 | Setup + Auth + Theme |
| Week 2 | Home + Dashboard |
| Week 3 | Lessons + Navigation |
| Week 4 | Quiz + Progress + Stars |
| Week 5 | Achievements + Profile |
| Week 6 | Admin Panel + Polish |

---

*PRD Created: April 2026*
*For: DeenQuest Laravel Project*