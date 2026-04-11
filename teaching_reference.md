# 📚 Teaching Reference Guide

This file explains how I teach you and the methodology behind each lesson so you can understand and help me improve.

---

## 🎯 Teaching Philosophy

### Core Principles

| Principle | Description |
|-----------|-------------|
| **Bilingual** | Always provide Bangla (বাংলা) + English versions |
| **Gamified** | Use stars ⭐, missions �MISSION, rewards 🏆 |
| **Child-friendly** | 10-year-old should understand everything |
| **Deep** | Real knowledge, not just memorization |
| **Interactive** | Quizzes, audio, visual elements when possible |
| **Trackable** | Easy to pick up where you left off |

---

## 📁 File Structure

```
DeenQuest/
├── teaching_reference.md
├── plan.md
├── day-1/
│   ├── learning.txt    # Content source
│   ├── readme.md       # Bangla version (REQUIRED)
│   ├── readme_en.md    # English version (REQUIRED)
│   ├── index.html      # Interactive HTML (REQUIRED)
│   └── learning.txt    # What to teach from
├── day-2/
│   └── ... (same structure)
├── ...
```

**IMPORTANT:** Every day folder MUST have:
1. `readme.md` - Bangla version
2. `readme_en.md` - English version
3. `index.html` - Interactive HTML version

### Why readme.md + readme_en.md?

GitHub auto-renders `readme.md` files, so anyone can learn directly from the repo without downloading.

---

## 📖 Lesson Format

Each day follows this structure:

1st read learning.txt in day folder and teach me by that and also you can add many more details information and try to make best interactive html for that lesson

### 1. Required Files for Each Day

For every day, you MUST create these 3 files:
- `readme.md` - Bangla version
- `readme_en.md` - English version  
- `index.html` - Interactive HTML version

### 2. Header Section (Required)
```
# 🌱 Islam Journey — Phase 1 / Day 1
## 🟢 Topic: Who is Allah?
```

### 2. Mission Statement
```
## 🎯 Today's Mission
- What we will learn today (bullet list)
```

### 3. Content Sections (in order)

| Section | Icon | Purpose |
|--------|------|---------|
| Knowledge | 🧠 | Core learning (who/what/why) |
| Heart | ❤️ | Emotional/spiritual connection |
| Eyes | 👀 | Important reminders |
| Game | 🎮 | Gamification activity |
| Memorization | 🧠 | Arabic/duas to memorize |
| Practice | 🛠️ | Tasks to do today |
| Character | ❤️ | Character building mission |
| Revision | 🔁 | Quick review of key points |
| Test | ⭐ | Tiny quiz to check understanding |
| Homework | 🏡 | Homework for tomorrow |
| Preview | 🚀 | Preview of next day |

### 4. Closing
```
---
**🎉 Great job! Day 1 Complete!**

Next: [Day 2 - ...](../day-2/readme.md)
```

---

## 🎮 Gamification Elements

| Element | How to Use | Example |
|---------|------------|---------|
| **Stars** ⭐ | Show earned stars for correct answers | ⭐⭐⭐⭐⭐ |
| **Missions** 🕵️ | Interactive detective/hunt games | "Universe Detective" |
| **Rewards** 🏆 | Give stars/badges for completion | 5 Stars Unlocked! |
| **Tasks** ✅ | Checkbox-style practice tasks | Task 1, Task 2, Task 3 |
| **Progress** 📊 | Track daily completion | Day 1 ☑️ Day 2 ☐ |

---

## 🎧 Audio/Video Elements

| Type | Format | When to Use |
|------|--------|-------------|
| **Quran recitation** | Audio player with Arabic | For memorization |
| **Translation** | Audio for meaning | For understanding |
| **Video** | Embed YouTube/link | For visual learners |
| **Image** | SVG/PNG | For knowledge graph |

### Audio Sources (AUTHENTIC):

**Quran Recitation:**
- QuranicAudio: https://www.quranicaudio.com
- Find specific surah: https://www.quranicaudio.com/quran/mp3/
- Format: `https://download.quranicaudio.com/quran/mp3/[reciter_name]/[surah_number].mp3`

**Famous Reciters:**
| Reciter | Folder Name | Notes |
|---------|------------|-------|
| Sheikh Mishary Al-Afasy | afasy | Popular, clear |
| Sheikh Abdul Basit | abdulbasit | Murattal |
| Sheikh Abdul Basit (Mujawwad) | AbdulBasit/Murattal | More tajweed |
| Sheikh Saad Al-Ghamdi | ghamdi | Beautiful voice |
| Sheikh Mahmoud Khalil Al-Husary | husary | Classic |

**Example Audio URLs:**
```
Surah Al-Fatiha (001): https://download.quranicaudio.com/quran/mp3/afasy_128kbps/001.mp3
Surah Al-Ikhlas (112): https://download.quranicaudio.com/quran/mp3/afasy_128kbps/112.mp3
```

**Duas:**
- Basira: https://www.basira.co.uk/duas/

### ⚠️ IMPORTANT: Audio Guidelines

1. **DO NOT use** `speechSynthesis` API - it produces unnatural Arabic pronunciation
2. **ALWAYS use** authentic Quran recitation from QuranicAudio.com or similar trusted sources
3. **Use embedded audio player** (HTML5 `<audio>` tag) for better user experience
4. **Provide direct MP3 links** from quranicaudio.com

### Audio Player Template:
```html
<audio id="audioPlayer" controls>
    <source src="https://download.quranicaudio.com/quran/mp3/afasy_128kbps/001.mp3" type="audio/mpeg">
    তোমার ব্রাউজার অডিও সাপোর্ট করে না
</audio>
<button onclick="document.getElementById('audioPlayer').play()">🔊 শুনো</button>
```

---

## 🧠 Content Guidelines

### Language Level

| Element | Rule |
|---------|------|
| **Vocabulary** | Simple, common words |
| **Sentence length** | Short (10-20 words) |
| **Examples** | From child life (toys, food, family, nature) |
| **No coding examples** | Use toys, games, nature instead |
| **Arabic** | Always with pronunciation + meaning |

### Content Depth

| Day Type | Content |
|----------|---------|
| Day 1 (concept) | Why + What + How |
| Day 2+ (details) | Deeper explanation |
| Revision days | Quick summary |
| Test days | Quiz + Assessment |

---

## 📅 Daily Routine Reference

### Recommended Daily Structure
- **Morning**: Review yesterday + Learn new lesson
- **Afternoon**: Practice tasks (throughout day)
- **Evening**: Homework + Tomorrow preview

### Time Estimates
| Activity | Time |
|----------|------|
| New lesson | 15-20 min |
| Memorization | 10 min |
| Practice tasks | Throughout day |
| Review | 5 min |

---

## 🔄 Progression System

### Phase Structure
1. **Phase 1** (Days 1-30): Foundation - Basic beliefs, salah, duas
2. **Phase 2** (Days 31-60): Worship - Wudu, salah, fasting
3. **Phase 3** (Days 61-90): Quran & Seerah - Deeper study
4. **Phase 4** (Days 91-120): Aqidah + Fiqh - Rules & beliefs
5. **Phase 5** (Days 121-180): Arabic + Tafsir - Language & interpretation
6. **Phase 6** (Days 181-365): Scholarship - Advanced topics

### Progress Indicators
- ☐ = Not started
- 🔄 = In progress  
- ✅ = Completed

---

## 🎓 Assessment Methods

### Informal (Daily)
- Quick questions after each lesson
- Practice task completion
- Character mission reflection

### Formal (Weekly/Monthly)
- Revision day quiz
- memorization check
- Phase test

---

## 💡 Tips for Me

If you want me to improve, tell me:

1. **Too fast?** → Slow down, more examples
2. **Too hard?** → Simpler words, more explanations
3. **Too easy?** → Add deeper content
4. **Need more audio?** → Add Arabic recitation
5. **Need more practice?** → Add more tasks

---

## 📞 How to Give Feedback

Just tell me:
- "This was too hard/easy"
- "I didn't understand X"
- "Can we add more examples of Y"
- "This format works well!"

---

**Last Updated:** Day 1
**For:** DeenQuest Islamic Learning Journey