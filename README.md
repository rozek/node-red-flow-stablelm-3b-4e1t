# node-red-flow-stablelm-3b-4e1t

Node-RED Flows for the StableLM-3B-4E1T AI model

This repository contains a function node for [Node-RED](https://nodered.org/) which can be used to run the [Stability AI](https://huggingface.co/stabilityai) [StableLM-3B-4E1T model](https://huggingface.co/stabilityai/stablelm-3b-4e1t) using [llama.cpp](https://github.com/rozek/llama.cpp) within a Node-RED flow. **Inference is done on the CPU** (without requiring any special harware) and still completes within a few seconds on a reasonably powerful computer.

![StableLM-3B-4E1T Text Completion Flow](./StableLM-3B-4E1T-Completion-Flow.png)

Additionally, this repo also contains function nodes to tokenize a prompt or to calculate embeddings based on the StableLM-3B-4E1T model.

Having the inference, tokenization and embedding calculation as a self-contained function node gives you the possibility to create your own user interface or even use it as part of an autonomous agent.

> Nota bene: these flows do not contain the actual model. You will have to download your own copy directly from [Huggingface](https://huggingface.co/rozek/StableLM-3B-4E1T_GGUF) (use file [stablelm-3b-4e1t-Q8_K.bin](https://huggingface.co/rozek/StableLM-3B-4E1T_GGUF/blob/main/stablelm-3b-4e1t-Q8_K.bin)).

> Just a small note: if you like this work and plan to use it, consider "starring" this repository (you will find the "Star" button on the top right of this page), so that I know which of my repositories to take most care of.

## Installation ##

This section shows you how to install Node.js, Node-RED, LLaMA.cpp and the flows from this repository - feel free to skip the steps for those components you already installed before.

### Node.js ###

"_[Node.js](https://nodejs.org/en) is a cross-platform, open-source server environment that can run on Windows, Linux, Unix, macOS, and more. Node.js is a back-end JavaScript runtime environment, runs on the V8 JavaScript engine, and executes JavaScript code outside a web browser._" (according to [Wikipedia](https://en.wikipedia.org/wiki/Node.js))

Start by [installing Node.js](https://nodejs.org/en) as described on their web page.

### Node-RED ###

"_[Node-RED](https://nodered.org/) is a flow-based, low-code development tool for visual programming developed originally by IBM..._" (according to [Wikipedia](https://en.wikipedia.org/wiki/Node-RED))

If not already done, install Node-RED as described on their "[Get Started](https://nodered.org/#get-started)" page.

### LLaMA.cpp ###

[LLaMA.cpp](https://github.com/ggerganov/llama.cpp) is a port of Facebook's LLaMA model in C/C++ (don't let you fool by the statement that the "_main goal of llama.cpp is to run the LLaMA model using 4-bit integer quantization on a MacBook_" - LLaMA.cpp runs just as well under Windows and Linux)

> Note: please use my own fork of the original LLaMA.cpp as the code in there raises the context limit and contains additional functions for tokenization - however, if you are fine with a context length of up to 4096 tokens and don't want to tokenize any prompts, the original code will work as fine

Get the code as follows:

```
git https://github.com/rozek/llama.cpp
cd llama.cpp
```

Then continue as described in the [LLaMA.cpp docs](https://github.com/rozek/llama.cpp#build)

Afterwards, rename the executables

* `main` to `llama`,
* `tokenization` to `llama-tokens` and
* `embedding` to `llama-embeddings`

and copy them into the Node-RED "User Directory" (by default, this folder is located at `$HOME/.node-red`).

### StableLM-3B-4E1T Flows ###

If not already done, download the [8-bit quantization of the StableLM-3B-4E1T model](https://huggingface.co/rozek/StableLM-3B-4E1T_GGUF/blob/main/stablelm-3b-4e1t-Q8_K.bin) into the same folder that already contains your executables.

> Nota bene: right now, the flows from this repository support the given model file only - if you prefer another one, you may simply change the model file name in the function nodes for text completion, tokenization and embeddings calculation.

Now import the desired nodes and flows - if you want them all, just import file [StableLM-3B-4E1T-Flows.json](https://raw.githubusercontent.com/rozek/node-red-flow-stablelm-3b-4e1t/master/StableLM-3B-4E1T-Flows.json).

If you are new to Node-RED, [just follow the instructions from their docs](https://nodered.org/docs/user-guide/editor/workspace/import-export).

## Usage ##

t.b.w

## Examples ##

If you have [cURL](https://curl.se/) installed (if not - but you want it - just [follow the instructions found in their docs](https://everything.curl.dev/get)) (and assuming that your Node-RED installation is listening at port 1880) you may use the following commands to "smoke test" the imported flows:

### Text Completion ###

```
curl "http://127.0.0.1:1880/stablelm?prompt=who%20was%20Joseph%20Weizenbaum%3F"
```

### Tokenization ###

```
curl "http://127.0.0.1:1880/stablelm-tokenization?prompt=who%20was%20Joseph%20Weizenbaum%3F"
```

### Embeddings Calculation ###

```
curl "http://127.0.0.1:1880/stablelm-embeddings?prompt=who%20was%20Joseph%20Weizenbaum%3F"
```

## License ##

[MIT License](LICENSE.md)
