# AI Learning Tracker - README

## Overview
**AI Learning Tracker** is an intelligent, privacy-first learning management system designed for senior embedded systems engineers preparing for interviews at top tech companies (Qualcomm, Mercedes-Benz, etc.). Track your study sessions, get AI-powered summaries, and receive personalized learning recommendations—all locally in your browser with zero cloud dependency.

## Features

### 📚 Session Logging
- **Date Selection**: Log sessions for any date (past or present)
- **Pre-built Topic Tags**: C++, Embedded Systems, AUTOSAR, CAN Bus, Linux Kernel, Cybersecurity, Interview Prep, Trading Bot
- **Custom Topics**: Add any topic not in the quick-select list
- **Flexible Duration**: Log in 0.5-hour increments
- **Rich Notes**: Capture detailed learning notes with full context

### 📊 Progress Dashboard
- **Total Hours**: Cumulative time invested across all sessions
- **Session Count**: Number of learning sessions logged
- **Unique Topics**: Diversity of topics studied
- **Weekly Goal Tracker**: Visual progress bar toward 20-hour weekly target
- **AI Recommendations**: Contextual next steps based on your recent learning

### 🤖 AI-Powered Insights
- **Smart Session Summaries**: AI analyzes your learning notes (when integrated with n8n)
- **Interview Prep Tips**: Embedded systems-specific recommendations
- **Topic Mastery Guidance**: Focused next steps for deeper understanding
- **Consistency Coaching**: Adaptive recommendations based on your learning patterns

### 📋 Session History
- **Recent Sessions View**: Latest 10+ sessions with date, topic, hours, and notes
- **Chronological Display**: Most recent sessions first
- **Quick Reference**: Truncated notes preview for quick scanning

### 🔒 Privacy & Local Storage
- **Browser-Only**: No server uploads, data stored in browser localStorage
- **Instant Access**: No login required
- **Portable**: Export/import your learning data anytime
- **GDPR Compliant**: Full user data control

---

## How to Use

### 1. **Log Your First Session**
   - Open the app in your browser
   - Date auto-fills to today
   - Click a **Quick Topic** tag (e.g., "C++") or type a **Custom Topic** (e.g., "AUTOSAR Layering")
   - Enter hours studied (e.g., 1.5)
   - Add detailed notes about what you learned
   - Click **Log Session**

### 2. **Track Your Progress**
   - View **Learning Progress** card for stats:
     - Total hours invested
     - Number of sessions
     - Topics covered
     - Weekly progress (goal: 20 hours/week)
   - AI recommendations update as you log more sessions

### 3. **Review Recent Sessions**
   - Scroll the **Recent Learning Sessions** section
   - See all logged sessions with date, topic, duration, and notes
   - Use browser search (Ctrl+F / Cmd+F) to find sessions by keyword

### 4. **Clear Data**
   - Click **Clear** button to reset the form
   - To delete all sessions: Open browser DevTools → Console → Run:
     ```javascript
     localStorage.removeItem('learningSessions');
     location.reload();
     ```

---

## Integration with n8n (Optional)

For **AI summaries, email notifications, and Google Sheets logging**, connect this tracker to your n8n workflow:

### Setup Steps:
1. **Import n8n workflow** from `n8n-learning-workflow.json`
2. **Configure credentials**:
   - Google Sheets API (for persistent logging)
   - OpenAI API (for AI summaries and recommendations)
   - Gmail SMTP (for email digests)
3. **Get webhook URL** from n8n and update the tracker:
   ```javascript
   // In logSession() function, add:
   fetch('https://your-n8n-instance/webhook/learning-log', {
       method: 'POST',
       headers: { 'Content-Type': 'application/json' },
       body: JSON.stringify({ date, topic, hours, notes, email: 'you@example.com' })
   })
   .then(r => r.json())
   .then(data => console.log('AI Summary:', data.summary));
   ```

### Benefits:
- ✅ Persist learning data to Google Sheets
- ✅ AI-generated session summaries (GPT-4)
- ✅ Daily email digests with recommendations
- ✅ Weekly analytics and insights
- ✅ Interview prep question generation

---

## Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Frontend** | Vanilla HTML5/CSS3/JS | No dependencies, instant performance |
| **Storage** | Browser localStorage | Client-side persistence |
| **Styling** | CSS Variables + Custom Design System | Responsive, accessible UI |
| **AI Integration** | OpenAI GPT-4 (via n8n) | Contextual learning insights |
| **Data Persistence** | Google Sheets (optional) | Backup and analytics |

---

## Recommended Learning Path

### Week 1-2: Foundations
- Topics: C++, Linux Kernel, CMake
- Target: 15+ hours
- Focus: Core language features, system calls, build tools

### Week 3-4: Embedded Systems
- Topics: AUTOSAR, CAN Bus, Real-time OS
- Target: 20+ hours
- Focus: Safety standards, communication protocols

### Week 5-6: Interview Prep
- Topics: Interview Prep, System Design, Debugging
- Target: 20+ hours
- Focus: Problem-solving, edge cases, optimization

### Week 7-8: Trading Bot (Optional Side Project)
- Topics: Trading Bot, Algorithm Design
- Target: 10+ hours
- Focus: Strategy implementation, backtesting

---

## Keyboard Shortcuts

| Action | Shortcut |
|--------|----------|
| Set today's date | Click date field → defaults to today |
| Quick topic select | Click any pre-built tag |
| Submit form | Ctrl+Enter (or click Log Session) |
| Clear form | Click Clear button |
| Search sessions | Ctrl+F (browser search) |
| Export data | Dev Console → `JSON.stringify(JSON.parse(localStorage.getItem('learningSessions')))` |

---

## Data Management

### Export Your Data
```javascript
// Run in browser console (F12)
const data = localStorage.getItem('learningSessions');
console.log(JSON.parse(data));
// Copy output to text file
```

### Import Data
```javascript
// Paste previously exported JSON
const newData = [ /* your data array */ ];
localStorage.setItem('learningSessions', JSON.stringify(newData));
location.reload();
```

### Backup Strategy
- **Weekly**: Export JSON via console, save to cloud (Google Drive, GitHub)
- **n8n Integration**: Auto-sync to Google Sheets for automatic backup

---

## Troubleshooting

### Sessions not saving?
- Check if localStorage is enabled (DevTools → Application → localStorage)
- Clear browser cache and reload
- Try private/incognito mode (data won't persist but will load)

### Stats not updating?
- Click a session, then refresh page
- Check browser console for errors (F12)
- Verify date format is YYYY-MM-DD

### AI recommendations not appearing?
- First: Log at least 3 sessions
- Second: Ensure n8n webhook is connected (optional)
- Without n8n: Static recommendations display based on session count

### Mobile not working well?
- Single-column layout auto-activates on phones
- Pinch to zoom if text is small
- Use portrait orientation for better UX

---

## Best Practices

✅ **Do:**
- Log sessions **immediately after** studying (while memory is fresh)
- Use **specific, measurable notes** (e.g., "Implemented CAN message parser in C++, tested with 5 protocols")
- Aim for **consistency**: 3-4 sessions/week minimum
- Review notes weekly to identify **knowledge gaps**
- **Export data monthly** as backup

❌ **Don't:**
- Log generic notes ("studied C++") — be specific
- Overestimate hours (log actual time, not intended time)
- Skip the custom topic if pre-built tags don't fit
- Delete old sessions — history matters for patterns
- Ignore AI recommendations — they're personalized to YOUR journey

---

## Credits & License

**Built for:** Senior embedded systems engineers preparing for top-tier interviews

**Technologies Used:**
- Design System: Custom CSS variables with accessibility focus
- State Management: Browser localStorage (zero dependencies)
- AI Integration: OpenAI GPT-4 (via n8n orchestration)

**License:** MIT (free to use, modify, distribute)

---

## Support & Feedback

For issues, feature requests, or integration help:
1. Check localStorage data: `localStorage.getItem('learningSessions')`
2. Test in incognito mode to isolate browser cache issues
3. Review n8n workflow for API configuration
4. Export data for manual debugging

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | Dec 2025 | Initial release: logging, stats, local storage, AI recommendations |
| 1.1 (Planned) | Q1 2026 | n8n integration, Google Sheets sync, mobile app |
| 2.0 (Roadmap) | Q2 2026 | Multi-user sync, spaced repetition, interview question bank |

---

**Happy learning! Track consistently, improve deliberately. Your interview success starts with capturing what you learn.** 🚀
