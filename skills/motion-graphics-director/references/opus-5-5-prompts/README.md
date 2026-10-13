# Opus 5.5 code-animation prompts

853 prompts people used to get Claude Opus 5.5 to write animations as code (HTML, Canvas, SVG, Three.js, shaders, GSAP). Vendored from [yihui-dev/awesome-opus5-5-videos](https://github.com/yihui-dev/awesome-opus5-5-videos) at commit `e6c7eee` (MIT, see `LICENSE`). Each video and prompt belongs to its creator, who is linked from `post_url`.

`videos.json` is a list of records with these fields: `slug`, `title`, `author`, `post_url`, `category` (`motion` 501, `3d` 123, `explainer` 122, `interactive` 107), `tech_tags` (canvas, svg, threejs, shader, gsap, css, audio, particles, playable, pixel, ai-image, webgl, physics), `prompt`, `prompt_partial` (true in 234 records where only part of the prompt was shared), `skillry_url`, `has_remake` and `added`.

To update it, re-copy `data/videos.json` from the upstream repo.
