# hey

Hey just translates user requests into shell commands:

```
$ hey what is the week day

Run date %A ? [Y/n]
Sunday
```

Even rude ones:
```
$ hey you

Run whoami ? [Y/n]
```

## Usage
Edit the Python file `hey`. It's small, and you normally only need to change the port. 
Copy it to PATH locations, e.g. `/usr/local/bin` and don't forget to `chmod u+x` it

## Backend
If you don't have a local LLM already grab llama.cpp and any small model 2-4B.
3-bit quants are ok if you are GPU/RAM poor. But I recommend 4B Q4_M. 
Tweaking the system prompt and temperature helps with small models.

```
brew install llama.cpp
llama serve -hf bartowski/Qwen_Qwen3.5-4B-GGUF:IQ3_XS -np 1 -c 2048 -ngl all \
	--chat-template-kwargs '{"enable_thinking":false}'
```

## Hey why? (why hey)
Idea isn't new, and there are a plenty of implementations... But those I tried turned out
to be slop, and running a full-blown agent with a tiny local model is overkill.
- The prompt is bloated and takes ages to process
- The prompt and inference parameters are fused into binary and can't be changed
- Megabytes of dependencies
- You need to CONFIGURE them and LEARN how to use

With `hey` you can easily modify the SYSTEM_PROMPT, by injecting more context
information e.g. `git status`. There's no session history or context compaction to care about.
