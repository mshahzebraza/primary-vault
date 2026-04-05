---
categories:
- '[[TechLearning]]'
tags:
- linux-pc-setup
---

```sh
pip3 install vosk && \
git clone https://github.com/ideasman42/nerd-dictation.git && \
cd nerd-dictation && \
wget https://alphacephei.com/kaldi/models/vosk-model-small-en-us-0.15.zip && \
unzip vosk-model-small-en-us-0.15.zip && \
mv vosk-model-small-en-us-0.15 model
```

If `pip` is not already installed, then you might need to run:
```bash
sudo apt install python3-pip
```

If faced with error: `externally managed environment`, then either we can bypass by using
`sudo apt install vosk` instead of `pip3 install vosk`.
