# node-red-flow-stablelm-3b-4e1t

Node-RED Flows for the StableLM-3B-4E1T AI model

This repository contains a function node for [Node-RED](https://nodered.org/) which can be used to run the [Stability AI](https://huggingface.co/stabilityai) [StableLM-3B-4E1T model](https://huggingface.co/stabilityai/stablelm-3b-4e1t) using [llama.cpp](https://github.com/rozek/llama.cpp) within a Node-RED flow. **Inference is done on the CPU** (without requiring any special harware) and still completes within a few seconds on a reasonably powerful computer.

![StableLM-3B-4E1T Text Completion Flow](./StableLM-3B-4E1T-Completion-Flow.png)

Additionally, this repo also contains function nodes to tokenize a prompt or to calculate embeddings based on the StableLM-3B-4E1T model.

Having the inference, tokenization and embedding calculation as a self-contained function node gives you the possibility to create your own user interface or even use it as part of an autonomous agent.

> Nota bene: these flows do not contain the actual model. You will have to download your own copy directly from [Huggingface](https://huggingface.co/rozek/StableLM-3B-4E1T_GGUF) (use file [stablelm-3b-4e1t-Q8_K.bin](https://huggingface.co/rozek/StableLM-3B-4E1T_GGUF/blob/main/stablelm-3b-4e1t-Q8_K.bin)).



## License ##

[MIT License](LICENSE.md)
