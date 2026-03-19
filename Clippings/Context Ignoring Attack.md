A **Context Ignoring Attack** <sup><span><a href="https://learnprompting.org/docs/prompt_hacking/offensive_measures/#footnote-label">1</a> <span><span><span>Liu, Y., Deng, G., Li, Y., Wang, K., Wang, Z., Wang, X., Zhang, T., Liu, Y., Wang, H., Zheng, Y., &amp; Liu, Y. (2024). Prompt Injection attack against LLM-integrated Applications. <a href="https://arxiv.org/abs/2306.05499">https://arxiv.org/abs/2306.05499</a></span></span></span></span></sup> is a more sophisticated form of [prompt injection](https://learnprompting.org/docs/prompt_hacking/injection) that attempts to make the LLM disregard its previous context and instructions. This attack combines elements of a [Simple Instruction Attack](https://learnprompting.org/docs/prompt_hacking/offensive_measures/simple-instruction-attack) <sup><span><a href="https://learnprompting.org/docs/prompt_hacking/offensive_measures/#footnote-label">2</a> <span><span><span>Schulhoff, S., Pinto, J., Khan, A., Bouchard, L.-F., Si, C., Anati, S., Tagliabue, V., Kost, A. L., Carnahan, C., &amp; Boyd-Graber, J. (2023). Ignore This Title and HackAPrompt: Exposing Systemic Vulnerabilities of LLMs through a Global Scale Prompt Hacking Competition. arXiv Preprint arXiv: 2311.16119. </span></span></span></span></sup> with specific directives designed to override the model's existing context.

The key strategy involves injecting a malicious prompt that explicitly instructs the LLM to ignore all preceding information and focus solely on the attacker's instructions. This makes it potentially more effective than basic prompt injection attempts.

Here's a simple example of such an attack:

When successful, this type of attack can cause the LLM to:

- Disregard its original training and safety constraints
- Bypass security measures put in place by the system
- Execute potentially harmful commands
- Reveal sensitive information it was instructed to keep private

A more advanced variation <sup><span><a href="https://learnprompting.org/docs/prompt_hacking/offensive_measures/#footnote-label">3</a> <span><span><span>Perez, F., &amp; Ribeiro, I. (2022). Ignore Previous Prompt: Attack Techniques For Language Models. <a href="https://arxiv.org/abs/2211.09527">https://arxiv.org/abs/2211.09527</a></span></span></span></span></sup> of this attack might look like:

The effectiveness of context ignoring attacks highlights the importance of implementing robust prompt security measures and proper input sanitization when developing LLM-based applications.