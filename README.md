# Exno.7-Develop a prompt-based application tailored to their personal needs, fostering creativity and practical problem-solving skills while leveraging the capabilities of large language models.

# Date:30/10/2025
# Register no: 212223220056
# Aim: To develop a prompt-based application using ChatGPT - To demonstrate how to create a prompt-based application to organize daily tasks, showing the progression from simple to more advanced prompt designs and their corresponding outputs.

# AI Tools Required: 
- Natural-language task input and organization.  
- Extraction of ACTION, TIME/DATE, PRIORITY, and REMINDER attributes.  
- Task management (add, list, update, delete).  
- Smart scheduling and conflict handling.  
- Context-aware wellness suggestions.  
- Adaptable tone and reminder settings based on feedback.  
- Basic memory to store user preferences and adapt behavior.


# Explanation: 
Prompt:
"Design a personal productivity assistant that can help manage daily tasks, schedule reminders, suggest wellness tips, and answer general queries. The assistant should interact using natural language and be adaptable to the user’s changing preferences over time."
Procedure:
1. Define the core requirements of a personal productivity assistant.
2. Identify and construct appropriate prompts for each task using an LLM (e.g., ChatGPT).
3. Simulate natural user interaction through a simple interface or command-line system.
4. Collect feedback or inputs from users and adapt responses accordingly.
5. (Optional) Integrate basic memory to simulate preference adaptation.
EXPECTED OUTPUT: - (attached the drive link)
Output (Example Response by LLM):
Personal Productivity Assistant Features:
1. Daily Task Manager:
o Accept tasks via natural language (e.g., "Remind me to call mom at 6 PM").
o Organize tasks by priority and deadline.
o Provide daily summaries and pending items.
2. Smart Scheduler:
o Schedule events and set reminders using contextual understanding.
o Notify user of overlapping appointments or free time slots.
3. Wellness Tips Generator:
o Suggest daily wellness advice (hydration, exercise, screen-time breaks).
o Adapt suggestions based on past user preferences and responses.

## 3. Procedure

### Step 1: Define Core Features
1. **Daily Task Manager** – Handle natural language inputs for reminders and tasks.  
2. **Smart Scheduler** – Schedule tasks, detect overlaps, and suggest alternate slots.  
3. **Wellness Tips Generator** – Provide short motivational and wellness messages.  
4. **Adaptive Feedback System** – Learn from user feedback to adjust tone and preferences.

### Step 2: Prompt Design

#### A. Task Extraction Prompt
```
You are an assistant that extracts structured task attributes from a user's natural language.
Return JSON with keys: intent, action, datetime, duration_minutes, priority, reminder_minutes, recurrence.
```

**Example Input:**
```
Remind me to call mom at 6 PM
```

**Example Output:**
```json
{
  "intent": "add_task",
  "action": "Call mom",
  "datetime": "2025-10-25T18:00:00+05:30",
  "duration_minutes": 15,
  "priority": "none",
  "reminder_minutes": 15,
  "recurrence": null
}
```

#### B. Confirmation Prompt
```
Using the extracted attributes, produce a friendly confirmation message.
Include ACTION, TIME, PRIORITY, and REMINDER. Use ≤3 emojis.
```
**Output:** Got it — I’ll remind you to call mom at 6:00 PM today ☎️

#### C. Listing and Conflict Handling Prompt
```
Return a short, clear list of all scheduled tasks and detect overlapping events.
```

#### D. Wellness Prompt
```
Suggest one short wellness action based on user state (e.g., tired, busy, stressed).
```

---

## 4. CLI Simulation

Below is a simple Python simulation that models assistant interactions:

```python
import datetime, json

tasks = []
session_memory = {"wake_up":"06:00","study_block_mins":120,"default_reminder":15}

def extract_attributes(text):
    text_l = text.lower()
    if "call" in text_l:
        return {"intent":"add_task","action":"Call mom","datetime":datetime.datetime.now().replace(hour=18,minute=0,second=0).isoformat(), "duration_minutes":15,"priority":"none","reminder_minutes":session_memory["default_reminder"],"recurrence":None}
    return None

def confirm_and_add(attrs):
    dt = attrs["datetime"]
    tasks.append(attrs)
    print(f"Got it — I'll remind you to {attrs['action']} at {dt} (Reminder: {attrs['reminder_minutes']} min before)")

def list_tasks():
    if not tasks:
        print("No tasks yet.")
        return
    for i,t in enumerate(tasks,1):
        print(f"{i}) {t['action']} — {t['datetime']} — Reminder:{t['reminder_minutes']}m")

def cli():
    while True:
        cmd = input("You: ")
        if cmd in ("quit","exit"): break
        if cmd.strip().lower().startswith("list"):
            list_tasks()
            continue
        attrs = extract_attributes(cmd)
        if attrs:
            confirm_and_add(attrs)
        else:
            print("Sorry, I didn't get that. Could you rephrase?")

if __name__ == "__main__":
    cli()
```

---

## 5. Expected Output

**Personal Productivity Assistant Features:**
- **Daily Task Manager**
  - Accept tasks via natural language (e.g., "Remind me to call mom at 6 PM").
  - Organize tasks by priority and deadline.
  - Provide daily summaries and pending items.
- **Smart Scheduler**
  - Schedule events and set reminders using contextual understanding.
  - Notify user of overlapping appointments or free time slots.
- **Wellness Tips Generator**
  - Suggest daily wellness advice (hydration, exercise, screen-time breaks).
  - Adapt suggestions based on past user preferences and responses.

---

## 6. Evaluation

| Metric | Description | Target |
|--------|--------------|--------|
| Extraction Accuracy | Correct parsing of ACTION, TIME, PRIORITY | ≥ 90% |
| Scheduling Efficiency | Conflict detection & rescheduling accuracy | ≥ 95% |
| User Satisfaction | Feedback average (👍/👎 ratio) | ≥ 85% positive |
| Adaptation Speed | Preference updates after feedback | Within 2 interactions |

---

## 7. Conclusion

This experiment demonstrates the creation of a **prompt-driven productivity assistant** using large language models. The assistant performs **task scheduling, wellness suggestion, and preference adaptation** with a natural conversational interface. Through structured prompts and feedback-based evolution, it becomes more personal and context-aware over time.



# Result: 
The lab exercise resulted in the creation of a prototype concept for a personal assistant powered by large language models. Students were able to:
 Understand how to tailor LLM prompts to real-life applications.
 Foster creativity by designing features suited to their personal or academic lives.
 Learn prompt engineering techniques for optimal interaction with AI tools.
 Experience the versatility and utility of generative AI in solving everyday problems.
