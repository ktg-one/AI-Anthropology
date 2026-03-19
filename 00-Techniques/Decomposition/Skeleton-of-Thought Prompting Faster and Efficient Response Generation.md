

Takeaways

- **Skeleton-of-Thought (SoT) prompting** enhances response generation by first creating a basic structure (skeleton) and then expanding it in parallel, reducing latency.
- **Two-stage process**: SoT divides generation into a skeleton phase followed by a detailed expansion phase, improving efficiency and speed.
- **Faster inference**: SoT delivers over 2x speed improvement on 8 out of 12 models, making it ideal for real-time applications.
- **Quality improvement**: In 60% of cases, SoT generates answers with quality equal to or better than traditional methods.
- **Limitations** include higher token usage costs and potential quality issues when points in the skeleton are interdependent.

## What is Skeleton-of-Thought Prompting?

Most state-of-the-art [Large Language Models (LLMs)](https://learnprompting.org/vocabulary/LLM) rely on [sequential decoding](https://learnprompting.org/vocabulary/sequential_decoding), which can lead to high latency. In contrast, humans approach problem-solving by first creating an outline or skeleton of their answer, then filling in details and supporting evidence.

**Skeleton-of-Thought (SoT) Prompting**<sup><span class="relative inline-block"><a href="https://learnprompting.org/docs/advanced/decomposition/#footnote-label" class="text-[#1D9774] no-underline hover:underline focus:outline-none">1</a><span class="absolute z-10 w-64 p-4 mt-2 text-sm bg-white dark:bg-gray-950 dark:border-2 dark:border-neutral-800 rounded-md shadow-lg ring-1 ring-black ring-opacity-5 transition-opacity duration-300 opacity-0 pointer-events-none" style="left: 50%; transform: translateX(-50%);"><span class="relative flex"><span class="text-gray-700 dark:text-gray-300 text-left w-5/6 popover-content ">Xuefei Ning. (2023). Skeleton-of-Thought: Prompting LLMs for Efficient Parallel Generation. </span><button class="absolute top-0 right-0 p-1 text-gray-400 dark:text-gray-300 hover:text-gray-600 hover:dark:text-gray-100 focus:outline-none" aria-label="Copy to clipboard"><svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="copy" class="svg-inline--fa fa-copy text-lg w-5 h-5" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"></path></svg></button></span></span></span></sup> mimics this parallel process. It first instructs the [LLM](https://learnprompting.org/vocabulary/LLM) to generate a basic answer structure (the skeleton), and then expands on each point to create a detailed response. To optimize for speed, the detailed generation phase uses parallel [API](https://learnprompting.org/vocabulary/api) calls or batched decoding, reducing latency compared to traditional methods.

## How to Use Skeleton-of-Thought Prompting?

SoT generates answers in two stages:

- Skeleton stage
- Point-expanding stage

### Skeleton Stage

In the skeleton stage, SoT utilizes the skeleton [prompt template](https://learnprompting.org/vocabulary/prompt_template) to generate a skeleton answer.


#### Prompt

---

\[User:\] You're an organizer responsible for only giving the skeleton (not the full content) for answering the question. Provide the skeleton in a list of points (numbered 1., 2., 3., etc.) to answer the question. Instead of writing a full sentence, each skeleton point should be very short with only 3~5 words. Generally, the skeleton should have 3~10 points. Now, please provide the skeleton for the following question.

{question}

Skeleton:

\[Assistant:\] 1.

This skeleton can be directly fed to LLM to get the skeleton answer.

Let's use SoT to gain tips on reducing carbon emissions on a personal level.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiMS4gUmVkdWNlIGVuZXJneSBjb25zdW1wdGlvblxuMi4gVXNlIHB1YmxpYyB0cmFuc3BvcnRhdGlvbi9jYXJwb29sXG4zLiBFYXQgbGVzcyBtZWF0XG40LiBTd2l0Y2ggdG8gcmVuZXdhYmxlIGVuZXJneVxuNS4gUGxhbnQgdHJlZXMvIHN1cHBvcnQgcmVmb3Jlc3RhdGlvbiIsInByb21wdCI6IllvdSdyZSBhbiBvcmdhbml6ZXIgcmVzcG9uc2libGUgZm9yIG9ubHkgZ2l2aW5nIHRoZSBza2VsZXRvbiAobm90IHRoZSBmdWxsIGNvbnRlbnQpIGZvciBhbnN3ZXJpbmcgdGhlIHF1ZXN0aW9uLlxuUHJvdmlkZSB0aGUgc2tlbGV0b24gaW4gYSBsaXN0IG9mIHBvaW50cyAobnVtYmVyZWQgMS4sIDIuLCAzLiwgZXRjLikgdG8gYW5zd2VyIHRoZSBxdWVzdGlvbi4gSW5zdGVhZCBvZiB3cml0aW5nIGEgZnVsbCBzZW50ZW5jZSwgZWFjaCBza2VsZXRvbiBwb2ludCBzaG91bGQgYmUgdmVyeSBzaG9ydCB3aXRoIG9ubHkgM341IHdvcmRzLiBHZW5lcmFsbHksIHRoZSBza2VsZXRvbiBzaG91bGQgaGF2ZSAzfjEwIHBvaW50cy4gTm93LFxucGxlYXNlIHByb3ZpZGUgdGhlIHNrZWxldG9uIGZvciB0aGUgZm9sbG93aW5nIHF1ZXN0aW9uLlxuV2hhdCBhcmUgc29tZSBwcmFjdGljYWwgdGlwcyBmb3IgaW5kaXZpZHVhbHMgdG8gcmVkdWNlIHRoZWlyIGNhcmJvbiBlbWlzc2lvbnM%2FIFxuU2tlbGV0b246IiwibW9kZWwiOiJncHQtMy41LXR1cmJvIn0%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

### Point-Expanding Stage

In this stage, SoT utilizes the point-expanding prompt template to expand the answer generated in the previous stage.

 

![Astronaut](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fastronaut.webp&w=48&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

#### Prompt

---

\[User:\] You're responsible for continuing the writing of one and only one point in the overall answer to the following question.

{question}

The skeleton of the answer is

{skeleton}

Continue and only continue the writing of point {point index}. Write it very short in 1~2 sentences and do not continue with other points!

\[Assistant:\] {point index}.{Point skeleton}

The LLM is fed with the points generated using the previous stage and is asked to expand one point at a time. This is repeated for all points in the skeleton. This process can be parallelized to speed up the inference.

- For LLMs with only [API](https://learnprompting.org/vocabulary/api) access, multiple parallel API requests can be sent to the provider.
- For LLMs running locally, inference can be optimized by performing the operations in batch.

Now, let's use the point-expanding prompt to expand our previous skeleton.

<iframe loading="lazy" src="https://embed.learnprompting.org/embed?config=eyJ0b3BQIjoxLCJ0ZW1wZXJhdHVyZSI6MC43LCJtYXhUb2tlbnMiOjI1Niwib3V0cHV0IjoiVHVybiBvZmYgbGlnaHRzIGFuZCBlbGVjdHJvbmljcyB3aGVuIG5vdCBpbiB1c2UsIHVucGx1ZyBjaGFyZ2VycywgYW5kIHVzZSBlbmVyZ3ktZWZmaWNpZW50IGFwcGxpYW5jZXMgdG8gbG93ZXIgeW91ciBvdmVyYWxsIGVuZXJneSBjb25zdW1wdGlvbi4iLCJwcm9tcHQiOiJZb3UncmUgcmVzcG9uc2libGUgZm9yIGNvbnRpbnVpbmcgdGhlIHdyaXRpbmcgb2Ygb25lIGFuZCBvbmx5IG9uZSBwb2ludCBpbiB0aGUgb3ZlcmFsbCBhbnN3ZXIgdG8gdGhlIGZvbGxvd2luZyBxdWVzdGlvbi5cbldoYXQgYXJlIHNvbWUgcHJhY3RpY2FsIHRpcHMgZm9yIGluZGl2aWR1YWxzIHRvIHJlZHVjZSB0aGVpciBjYXJib24gZW1pc3Npb25zPyBcblRoZSBza2VsZXRvbiBvZiB0aGUgYW5zd2VyIGlzXG4xLiBSZWR1Y2UgZW5lcmd5IGNvbnN1bXB0aW9uXG4yLiBVc2UgcHVibGljIHRyYW5zcG9ydGF0aW9uL2NhcnBvb2xcbjMuIEVhdCBsZXNzIG1lYXRcbjQuIFN3aXRjaCB0byByZW5ld2FibGUgZW5lcmd5XG41LiBQbGFudCB0cmVlcy8gc3VwcG9ydCByZWZvcmVzdGF0aW9uXG5cbkNvbnRpbnVlIGFuZCBvbmx5IGNvbnRpbnVlIHRoZSB3cml0aW5nIG9mIHBvaW50IDEuIFdyaXRlIGl0ICoqdmVyeSBzaG9ydGx5KiogaW4gMX4yIHNlbnRlbmNlIGFuZCBkbyBub3QgY29udGludWUgd2l0aCBvdGhlciBwb2ludHMhXG5cbjEuIFJlZHVjZSBlbmVyZ3kgY29uc3VtcHRpb246IiwibW9kZWwiOiJncHQtMy41LXR1cmJvIn0%3D" sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts" style="width: 100%; height: 500px; border: 0px; border-radius: 4px; overflow: hidden;"></iframe>

## What Are Skeleton-of-Thought Prompting Results?

- On 8 out of 12 models, SoT obtains a speed-up of at least 2x.

![Speed-up gained using SoT](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fspeed_up.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Speed-up gained after employing SoT (Ning et al.)

- The quality of answers generated by SoT is either comparable or better than that of normal generation in 60% of the cases.

![Quality evaluation of answers generated using SoT](https://learnprompting.org/_next/image?url=%2Fdocs%2Fassets%2Fadvanced%2Fanswer_quality.webp&w=3840&q=75&dpl=dpl_4xrNJubb2rB1yNq1SNnQqJtckvvd)

Quality evaluation across two metrics: FastChat and LLMZoo (Ning et al.)

## Limitations of Skeleton-of-Thought Prompting

- The quality of generated answers using the SoT approach was evaluated using GPT-4 judges without any involvement of human experts. Hence, the answer quality evaluation isn't perfect.
- SoT doesn't consider dependencies between points in the skeleton. As a result, when there is interdependence between points in the skeleton, the generated detailed answer may not be comprehensive.
- LLMs available via API are charged depending on the token usage. Employing SoT may increase token usage and, hence, the bills.

## Conclusion

SoT can boost the inference speed of the model by over 2 times using parallelization. SoT is easy to implement and can be implemented with a few simple modifications to any prompt. However, the quality of the generated response may not be optimal, and humans need to evaluate it before deciding to use SoT in a production environment.

Find more on [Decomposition Prompting](https://learnprompting.org/docs/advanced/decomposition/introduction) methods.