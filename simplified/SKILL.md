[SKILL.md](https://github.com/user-attachments/files/34729993/SKILL.md)
---
name: simplified
description: Explain any topic in Simplified Technical English (ASD-STE100 style) with a fixed skimmable structure. Use when the user types /simplified or asks for a simplified explanation.
---

# Simplified

Explain the topic in clear English. Accuracy comes first: make the words simple, not the facts.

## Step 1: Pick the mode
If the first word after `/simplified` is a mode name (`/simplified deep F-22`), use that mode and do not ask. Otherwise ask one multiple-choice question with AskUserQuestion (header "Mode"). The tool allows only 4 options, so list these 4 and mention in the question text that they can type "quick" for a 2-3 sentence answer:
- **Textbook**: normal detailed paragraphs with the most facts
- **Flow**: short manual-style paragraphs you read straight through
- **Structured**: labeled sections you can scan
- **Deep**: significance plus who/what/when/where/why/how

If no question tool is available, use Structured.

## Writing rules (all modes except Textbook, ASD-STE100 base)
- Max 20 words per sentence. One idea per sentence.
- Active voice. Present tense where possible.
- Use the same word for the same thing every time.
- No idioms, filler, hedging, or intro sentences.

## Reader and terms (all modes)
- Assume a smart reader with a good general vocabulary who is new to this field.
- On first use, explain each field-specific term, name, or acronym inline in parentheses: "F-22 (a US stealth fighter jet)", "ASD-STE100 (the simplified English used in aircraft manuals)".
- Never explain everyday or general-vocabulary words. If an educated adult outside the field knows it, leave it alone.
- If the topic is ambiguous (it has more than one meaning), say in one line which meaning you used, then continue.

## Modes

**Textbook**
- Normal, well-written English paragraphs. The STE writing rules do not apply, but cut filler and intro sentences.
- Give the most complete picture: include advanced details, numbers, and edge cases (for example, relativity corrections for GPS).
- 3-6 paragraphs in a logical order.
- End with **Remember:** one line to keep.

**Flow**
- 3-6 short paragraphs in the order things happen or connect.
- End with **Remember:** one line to keep.

**Structured**
1. **Answer:** one sentence with the core idea.
2. **How it works:** 3-7 numbered steps, in the order they happen.
3. **Example:** one concrete real-world example, with a real number if one fits.
4. **Watch out:** one common misunderstanding or important detail people miss.
5. **Remember:** one line the reader should keep.

**Deep**
1. **Answer:** one sentence with the core idea.
2. **Why it matters:** the significance: what it changed, what depends on it, why anyone should care.
3. **What / Who / When / Where:** short lines for each. Skip any W that does not fit the topic (for example, "who" for a math concept).
4. **How it works:** numbered steps, in order.
5. **Why it works this way:** the reason behind the design or cause, plus the main tradeoff.
6. **Watch out:** one common misunderstanding.
7. **Remember:** one line to keep.

**Quick**
- 2-3 sentences with the core idea and the single most important detail. Then **Remember:** one line.

## Depth and length
- Keep every fact that changes how the thing works, even if it is advanced. State it in simple words.
- Length: Quick under 60 words, Flow and Structured under 250, Textbook under 350, Deep under 450.
- If the user says "deeper", add a **More detail** section in the same mode.
- If a picture would explain it faster (a process, a system, a comparison), offer a diagram in one line at the end.
