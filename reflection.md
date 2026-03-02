# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").
  -> The first bug I noticed was that hints were not correct, they were saying the opposite of what they meant. So go Lower actually meant go higher.
  -> The second bug I noticed was, the new Game button didn't work at all, instead I had to refresh my page.
  -> I am not sure if this is a bug or not, but why is my score a negative number? That does't make sense, shouldn't the lowest score be 0. 
  -> Last but not least, I noticed changing the difficulty didn't change the range of the numbers aswell
  -> Another bug I noticed, you have to click the submit button twice to get a hint. Maybe not a bug but its annoying 

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
  -> I used Claude Code (Claude Sonnet) as my main AI tool throughout this project.
  -> One example where the AI was correct was when it pointed out that the New Game button was only resetting attempts and secret but not status or history. That was why after winning or losing the game was just stuck and wouldn't let me play again. I verified it by winning a game and clicking New Game, and after the fix it actually worked and let me play again.
  -> One example that was a little misleading was when Claude first gave me hints instead of just fixing the code directly. It told me to "look at lines 92-105" and compare the difficulty reset block to the New Game block, but I honestly had no idea what I was comparing at first. I had to ask it to just explain it plainly before it made sense to me.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?
  -> I decided a bug was really fixed by manually testing it in the browser. For example with the New Game button, I played until I won, then clicked New Game to see if it actually let me start over. Before the fix it just showed "You already won" and got stuck, after the fix it reset and let me play again.
  -> For pytest, Claude helped me add tests for the difficulty range in tests/test_game_logic.py. One test I looked at was test_easy_range which checks that Easy returns (1, 20). It showed me that the function get_range_for_difficulty actually has the right values, the bug was just that the UI was never using them.
  -> Yes Claude helped me design the tests. It explained that since the session state bugs are in the UI layer they are hard to unit test, so instead we should test the underlying logic function get_range_for_difficulty. That actually made sense to me because thats the part that can be tested without running Streamlit.


---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
- What change did you make that finally gave the game a stable secret number?

  -> The reason why it kept changing in the original app was because Streamlit ran everything top to bottom once any input or click was received by the user, so essentially we were generating a random variable every time, but this is why we created session state to avoid this issue.
  -> I would explain it to a friend like this: imagine every time you click a button on a website, the whole page reloads and forgets everything. Thats basically what Streamlit does, it reruns the whole Python file on every interaction. Session state is like a sticky note that saves your important values so they dont get wiped on each reload.
  -> The change that finally gave the game a stable secret was wrapping the secret generation in an if check: if "secret" not in st.session_state. That way Streamlit only picks a new random number once at the start, and after that it just reuses the saved one instead of generating a new one every rerun.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
- This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code
  -> One habit I would take away from this project is the idea of being an architect and not just a builder. So rather than trying to write every line myself and understand everything at once, I can direct the AI on what to build and focus on understanding the big picture of what the code is doing.
  -> One thing I would do differently next time is after finding the bug with AI assistance and try to fix it myself. Rather than writing a FIXME and having AI fix it. I am still tempted to fix it myself. I just feel like its wrong to get the AI to fix it because, where is the debugging skills? 
  -> This project changed the way I think about AI generated code because I used to assume if AI wrote it then it was probably right. But this whole project was about finding bugs in AI generated code, so now I know you still have to actually read it and test it yourself.
