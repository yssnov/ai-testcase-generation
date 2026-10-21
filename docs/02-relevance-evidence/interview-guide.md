# Interview guide (online chat, 5 questions)

Russian version used in the interviews: [interview-guide-ru.md](interview-guide-ru.md).

**Goal:** find out which part of a QA engineer's work is the most painful or tedious and needs relief. It may be something other than test design; that answer is equally valuable.

**Principle:** ask only about **past experience and specific cases**, not future intentions. Do not ask about our product: "would you use it?" gets a polite "yes" and proves nothing.

**Format:** online text chat (Telegram, WhatsApp, LinkedIn). Follow-up questions are built into each question because immediate clarification is harder in chat.

## Opening message

> Hello, [name]! I am a student at Astana IT University; our diploma project is about how QA engineers work. We are not selling anything. May I ask you 5 short questions about your experience here in the chat? Answers are anonymous: we do not publish your name or company. You may skip any question.

The message deliberately avoids the words "test cases" and "requirements" so as not to suggest the expected answer.

## Questions (one message each; the next one after the answer)

1. Think about your last working week: which tasks took most of your time? Which of them was the most tedious or annoying? → main pain, whatever it is (H8, H1)
2. Tell me about the last feature you tested: in what form did the requirements come (Jira, Confluence, Word, verbally…), in which language, and roughly how many hours did preparation take before the first test run? → where requirements live, time, language (H1, H6, H7)
3. Think of the last time a bug reached production or work had to be redone. What happened and why was it not caught earlier? → where gaps come from, without suggested answers (H2, H4)
4. Have you or your colleagues tried AI (ChatGPT, Copilot, etc.) or other tools to speed up any part of your work? What worked, what got in the way? Are there company rules about what may be sent to external services? → cloud-AI restrictions and experience (H3, H5)
5. Is there anything in your work you have already tried to simplify yourself — scripts, templates, checklists, macros? What exactly, and did it help? → if a person already spent time on it, the pain is real (H8)

## Closing message

> Thank you very much, this helped a lot! May we contact you later when we have a prototype to show it and hear your opinion?

If asked about the diploma topic, answer in one sentence and only after question 5.

## Rules

- Send one question at a time; all five at once only if the respondent asks.
- If an answer is general ("usually", "it depends"), ask: "Could you give an example from the last time?"
- If the respondent names a pain unrelated to test cases, ask: "Could you tell more about what exactly takes the time?" — a valuable result.
- Do not agree or comment ("yes, that's a problem!"); reply neutrally: "Got it, thank you."
- Keep the chat log (screenshot or text) privately, outside Git.

## After the interview

- Within 24 hours fill in the [notes template](interview-notes-template.md); mark each statement as **fact** (what actually happened) or **opinion** (what they think or would like).
- No company or personal names in the repository: "P?, QA engineer, <industry>, N years" (e.g. telecom, bank, outsourcing).
- Do not accept real internal requirement documents (constraint C-03).
