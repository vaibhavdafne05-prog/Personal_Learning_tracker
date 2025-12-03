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
- **Batch Logging**: Quick-add multiple sessions in succession with pre-filled topics

### 📊 Progress Dashboard
- **Total Hours**: Cumulative time invested across all sessions
- **Session Count**: Number of learning sessions logged
- **Unique Topics**: Diversity of topics studied
- **Weekly Goal Tracker**: Visual progress bar toward 20-hour weekly target
- **AI Recommendations**: Contextual next steps based on your recent learning
- **Streak Counter**: Track consecutive days with logged sessions (coming soon)
- **Topic Deep Dive**: Click topics to see detailed mastery progression

### 🤖 AI-Powered Insights
- **Smart Session Summaries**: AI analyzes your learning notes (when integrated with n8n)
- **Interview Prep Tips**: Embedded systems-specific recommendations for Qualcomm/Mercedes-Benz
- **Topic Mastery Guidance**: Focused next steps for deeper understanding
- **Consistency Coaching**: Adaptive recommendations based on your learning patterns
- **Knowledge Gap Detection**: AI identifies areas needing reinforcement
- **Interview Question Generation**: Auto-generate practice questions from your learning history

### 📋 Session History
- **Recent Sessions View**: Latest 10+ sessions with date, topic, hours, and notes
- **Chronological Display**: Most recent sessions first
- **Quick Reference**: Truncated notes preview for quick scanning
- **Session Search & Filter**: Find sessions by topic, date range, or keyword
- **Session Export**: Download individual sessions as JSON
- **Bulk Operations**: Delete, archive, or tag multiple sessions

### 🔒 Privacy & Local Storage
- **Browser-Only**: No server uploads, data stored in browser localStorage
- **Instant Access**: No login required
- **Portable**: Export/import your learning data anytime
- **GDPR Compliant**: Full user data control
- **Encryption Ready**: Built for easy encryption layer addition (coming v1.1)
- **Device Sync**: WebSync bridge for multi-device localStorage (coming v1.2)

---

## How to Use

### 1. **Log Your First Session**
   - Open the app in your browser
   - Date auto-fills to today
   - Click a **Quick Topic** tag (e.g., "C++") or type a **Custom Topic** (e.g., "AUTOSAR Layering")
   - Enter hours studied (e.g., 1.5)
   - Add detailed notes about what you learned (include key concepts, problems solved, blockers)
   - Click **Log Session**
   - *Tip: Include code snippets or command outputs in notes for richer AI analysis*

### 2. **Track Your Progress**
   - View **Learning Progress** card for stats:
     - Total hours invested
     - Number of sessions
     - Topics covered
     - Weekly progress (goal: 20 hours/week)
   - AI recommendations update as you log more sessions
   - **Weekly Review**: Every Monday, review last week's topics and gaps

### 3. **Review Recent Sessions**
   - Scroll the **Recent Learning Sessions** section
   - See all logged sessions with date, topic, duration, and notes
   - Use **Filter by Topic** to see mastery progression on specific areas
   - Use browser search (Ctrl+F / Cmd+F) to find sessions by keyword
   - *Pro Tip: Search for "blocker" or "error" to review challenging sessions*

### 4. **Export & Backup**
   - Click **Export Data** to download all sessions as JSON
   - Save to Google Drive / GitHub weekly
   - Use **Import Data** to restore from backup

### 5. **Clear Data**
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
   - Pinecone or Weaviate (for semantic search of past sessions—optional)
3. **Get webhook URL** from n8n and update the tracker:
   ```javascript
   // In logSession() function, add:
   fetch('https://your-n8n-instance/webhook/learning-log', {
       method: 'POST',
       headers: { 'Content-Type': 'application/json' },
       body: JSON.stringify({ date, topic, hours, notes, email: 'you@example.com' })
   })
   .then(r => r.json())
   .then(data => {
       console.log('AI Summary:', data.summary);
       showAlert('Session logged & analyzed by AI', 'success');
   });
   ```

### Benefits:
- ✅ Persist learning data to Google Sheets with automatic versioning
- ✅ AI-generated session summaries (GPT-4) with interview context
- ✅ Daily email digests with actionable recommendations
- ✅ Weekly analytics dashboard (Looker Studio integration)
- ✅ Interview prep question generation from your learning history
- ✅ Spaced repetition reminders (coming v1.2)
- ✅ Semantic similarity search across all sessions

---

## Tech Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Frontend** | Vanilla HTML5/CSS3/JS | No dependencies, instant performance, <50KB total |
| **Storage** | Browser localStorage | Client-side persistence, unlimited reads/writes |
| **Styling** | CSS Variables + Custom Design System | Responsive, accessible UI (WCAG AA compliant) |
| **AI Integration** | OpenAI GPT-4 / Claude 3 (via n8n) | Contextual learning insights, multi-model support |
| **Data Persistence** | Google Sheets (optional) | Backup, analytics, multi-device sync |
| **Search** | Pinecone / Weaviate (optional) | Semantic similarity for finding related sessions |
| **Notifications** | Gmail SMTP / Slack (optional) | Email digests, Slack daily summaries |

---

## Recommended Learning Path

### Week 1-2: Foundations
- Topics: C++, Linux Kernel, CMake
- Target: 15+ hours
- Focus: Core language features, system calls, build tools
- **Interview Angles**: Memory management, RAII, thread safety
- **Practice**: LeetCode medium C++ problems, system call exploration

### Week 3-4: Embedded Systems Fundamentals
- Topics: Embedded Systems, AUTOSAR, CAN Bus, Real-time OS
- Target: 20+ hours
- Focus: Safety standards (ISO 26262), communication protocols, timing constraints
- **Interview Angles**: Real-time scheduling, interrupt handling, hardware abstraction
- **Practice**: Design CAN message handlers, AUTOSAR layer implementation

### Week 5-6: Advanced Topics & System Design
- Topics: Cybersecurity, Linux Kernel deep-dive, System Architecture
- Target: 20+ hours
- Focus: Threat modeling, kernel modules, system design trade-offs
- **Interview Angles**: Security vulnerabilities in automotive, performance optimization
- **Practice**: Design a secure automotive communication stack

### Week 7-8: Interview Prep & Trading Bot
- Topics: Interview Prep, System Design, Trading Bot (optional)
- Target: 20+ hours
- Focus: Problem-solving frameworks, edge cases, live coding practice
- **Interview Angles**: Behavioral (team leadership), technical depth, system thinking
- **Practice**: Mock interviews 3x/week, design system problems daily

---

## Keyboard Shortcuts

| Action | Shortcut |
|--------|----------|
| Set today's date | Click date field → defaults to today |
| Quick topic select | Click any pre-built tag (hold Shift for multi-select) |
| Submit form | Ctrl+Enter (or click Log Session) |
| Clear form | Click Clear button or Ctrl+Shift+L |
| Search sessions | Ctrl+F (browser search) |
| Filter by topic | Click topic in session → shows all sessions on that topic |
| Export data | Ctrl+E (browser console → copy JSON) |
| Delete session | Swipe right on mobile, right-click on desktop |
| Add tag to session | Click "+" on existing session (v1.1) |

---

## Data Management

### Export Your Data
```javascript
// Run in browser console (F12)
const data = localStorage.getItem('learningSessions');
const json = JSON.parse(data);
console.log(json);
// Right-click → Save as "learning_backup_YYYY-MM-DD.json"
```

### Import Data
```javascript
// Paste previously exported JSON
const newData = [ /* your data array */ ];
localStorage.setItem('learningSessions', JSON.stringify(newData));
location.reload();
```

### Backup Strategy
- **Weekly**: Export JSON via console, save to Google Drive/GitHub
- **Monthly**: Verify import works with a backup on fresh device
- **n8n Integration**: Auto-sync to Google Sheets for automatic versioned backup
- **Version Control**: Store backups in git with timestamps

### Data Migration
```bash
# Export all sessions
open DevTools → Console → copy output
# Save as learning_sessions.json in repo
# Commit with message: "Backup: [date] [topic count]"
```

---

## Advanced Features (Coming Soon)

### v1.1 (Q1 2026)
- **Session Tagging**: Add custom tags (e.g., #blocker, #breakthrough, #review)
- **Topic Mastery Levels**: Track progression from Beginner → Advanced → Expert
- **Spaced Repetition**: AI suggests reviewing sessions at optimal intervals
- **Interview Question Bank**: Auto-generate practice questions from your notes
- **Data Encryption**: End-to-end encryption for sensitive learning data
- **Mobile App**: Native iOS/Android with offline sync

### v2.0 (Q2 2026)
- **Multi-Device Sync**: Seamless sync across laptop, tablet, phone
- **Collaborative Learning**: Share sessions with study group, get peer feedback
- **Video Integration**: Link YouTube videos to sessions, extract timestamps
- **Analytics Dashboard**: Heat maps of learning intensity, topic correlation analysis
- **Interview Simulator**: AI-powered mock interviews with your learning context
- **Certification Tracking**: Auto-track progress toward AWS, AUTOSAR, ASIL certifications

---

## Troubleshooting

### Sessions not saving?
- Check if localStorage is enabled (DevTools → Application → localStorage)
- Clear browser cache and reload
- Try private/incognito mode (data won't persist but will load)
- **Solution**: Use Firefox if Chrome localStorage is corrupted

### Stats not updating?
- Click a session, then refresh page
- Check browser console for errors (F12)
- Verify date format is YYYY-MM-DD
- **Solution**: Clear localStorage and re-import backup

### AI recommendations not appearing?
- First: Log at least 3 sessions
- Second: Ensure n8n webhook is connected (optional)
- Without n8n: Static recommendations display based on session count
- **Solution**: Check n8n logs for webhook errors

### Mobile not working well?
- Single-column layout auto-activates on phones
- Pinch to zoom if text is small
- Use portrait orientation for better UX
- **Solution**: Use Firefox mobile or Safari mobile for best compatibility

### Data lost after browser update?
- Browser updates sometimes clear localStorage
- **Prevention**: Export data weekly to Google Drive
- **Recovery**: Use Google Drive version history to restore backups

---

## Best Practices

✅ **Do:**
- Log sessions **immediately after** studying (while memory is fresh)
- Use **specific, measurable notes** (e.g., "Implemented CAN message parser in C++, tested with 5 protocols, fixed race condition in interrupt handler")
- Include **code snippets** in notes for later reference
- Aim for **consistency**: 3-4 sessions/week minimum (better: daily 1-2h sessions)
- Review notes **weekly** to identify knowledge gaps
- **Export data monthly** as backup to Google Drive
- Link related sessions with topic tags (coming v1.1)
- Document **blockers and breakthroughs** explicitly for AI analysis

❌ **Don't:**
- Log generic notes ("studied C++") — be specific with outcomes
- Overestimate hours (log actual time, not intended time)
- Skip the custom topic if pre-built tags don't fit — detail matters
- Delete old sessions — history reveals learning patterns
- Ignore AI recommendations — they're personalized to YOUR journey
- Log while distracted — focus = quality notes
- Skip reflection — 2min reflection note per session improves retention 5x

---

## Performance Tips

**Optimize for Speed:**
- Clear localStorage every 6 months (archive to JSON first)
- Use incognito mode if you have >500 sessions (faster rendering)
- For large exports, use a text editor (not Google Sheets) initially
- On mobile: use Chrome over Safari (faster localStorage)

**Optimize for Learning:**
- Log sessions **same time daily** (builds habit)
- Review last week's topics every Monday (spaced repetition)
- Tag sessions with difficulty (Easy/Medium/Hard) manually (v1.1 feature)
- Link to relevant interview resources in notes

---

## Credits & License

**Built for:** Senior embedded systems engineers preparing for top-tier interviews (Qualcomm, Mercedes-Benz, Bosch, Tesla, etc.)

**Inspiration:** Spaced repetition (Anki), deliberate practice (Cal Newport), learning tracking (Obsidian)

**Technologies Used:**
- Design System: Custom CSS variables with accessibility focus (WCAG AA)
- State Management: Browser localStorage (zero dependencies)
- AI Integration: OpenAI GPT-4 (via n8n orchestration)

**License:** MIT (free to use, modify, distribute)

---

## Support & Feedback

For issues, feature requests, or integration help:

1. **Check Storage First**: 
   ```javascript
   localStorage.getItem('learningSessions')
   ```

2. **Debug in Console** (F12):
   ```javascript
   console.log('Total sessions:', JSON.parse(localStorage.getItem('learningSessions')).length);
   ```

3. **Test Isolation**:
   - Try incognito mode to isolate browser cache issues
   - Use Firefox if Chrome has issues
   - Clear site data: Settings → Privacy → Clear browsing data

4. **n8n Troubleshooting**:
   - Verify webhook URL is active: POST to webhook with test data
   - Check n8n logs for API errors
   - Confirm OpenAI/Google Sheets credentials are valid

5. **Data Recovery**:
   - Check Google Drive backups
   - Use browser history to find previous session data
   - Contact support with localStorage export (sanitized)

---

## Community & Resources

**Interview Prep Resources:**
- LeetCode Hard C++ problems (daily 1-2)
- AUTOSAR specification (free ISO draft)
- CAN Bus protocol deep-dive (Vector docs)
- Linux kernel source code (kernel.org)

**Community Learning:**
- Join embedded systems Discord servers
- Contribute to open-source automotive projects (OpenDLV, AUTOSAR examples)
- Start learning group with 2-3 peers
- Share session summaries on LinkedIn for accountability

**Interview Success Stories:**
- Document your 8-week learning journey
- Share template with others preparing
- Build in public: post weekly progress on Twitter/LinkedIn
- Connect with others using this tracker

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | Dec 2025 | Initial release: logging, stats, local storage, AI recommendations, n8n integration |
| 1.1 (Planned) | Q1 2026 | Session tagging, mastery levels, spaced repetition, interview Q bank, encryption, mobile app |
| 1.2 (Roadmap) | Q2 2026 | Multi-device sync (WebSync), collaborative learning, video integration, analytics, mock interviews |
| 2.0 (Vision) | Q3 2026 | Professional certifications, team dashboard, enterprise integrations, AI tutoring |

---

## FAQ

**Q: Can I use this without n8n?**
A: Absolutely! The tracker works fully offline. n8n is optional for AI summaries and email digests.

**Q: Is my data safe?**
A: Yes. Data never leaves your browser. It only leaves if you enable n8n + Google Sheets integration.

**Q: Can I share this with my study group?**
A: Absolutely! Tracker is MIT licensed. Each person gets their own localStorage (not shared).

**Q: How long until I'm interview-ready?**
A: 8-12 weeks of consistent 15-20h/week = ready for interviews. Quality > Quantity.

**Q: Can I integrate with Obsidian / Notion?**
A: Yes (coming v1.1). n8n can sync to Obsidian via GitHub Automator or Notion API.

---

**Happy learning! Track consistently, improve deliberately. Your interview success starts with capturing what you learn.** 🚀

**Current Status:** 🟢 Production Ready | 📈 Active Development | 🤝 Community Driven
