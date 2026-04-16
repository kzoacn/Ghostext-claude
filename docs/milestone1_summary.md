# Milestone 1: Initial Investigation Summary

## Codebase Exploration

The Ghostext project is located in `../Ghostext` and contains a complete implementation of a text steganography system using LLMs and arithmetic coding.

### Key Components

1. **CLI Interface** (`cli.py`)
   - Provides `encode` and `decode` commands
   - Supports both llama-cpp backend and toy backend (for testing)
   - Outputs JSON with statistics when `--json` flag is used

2. **Encoder** (`encoder.py`)
   - Encrypts plaintext and embeds it into generated text
   - Uses arithmetic coding to map encrypted bits to token choices
   - Supports retry mechanism for low-entropy situations

3. **Decoder** (`decoder.py`)
   - Extracts hidden message from stego text
   - Uses same model, prompt, passphrase, and seed as encoder

4. **Crypto Layer** (`crypto.py`)
   - Uses scrypt for key derivation
   - Uses ChaCha20-Poly1305 for AEAD encryption
   - Packet structure: salt | header_nonce | sealed_header | body_nonce | body_ciphertext

5. **Model Backend** (`llama_cpp_backend.py`)
   - Default backend: Qwen3.5-2B (GGUF format)
   - Provides tokenization and next-token distribution

6. **Codec** (`codec.py`)
   - Implements arithmetic/range coding
   - Quantizes probabilities to integer frequencies

7. **Candidate Policy** (`candidate_policy.py`)
   - Filters candidates based on top-p and max_candidates
   - Ensures retokenization stability

### Configuration Defaults

- seed: 7
- ctx_size: 4096
- batch_size: 128
- top_p: 0.995
- max_candidates: 64
- min_entropy_bits: 0.0
- totfreq: 4096
- natural_tail_max_tokens: 64
- low_entropy_window_tokens: 32
- low_entropy_threshold_bits: 0.1
- max_encode_attempts: 10

## Test Results

### Test 1: English short message
- Prompt: "Write a short, natural paragraph about a quiet evening walk."
- Message: "Attack at Dawn!"
- Packet length: 103 bytes
- Total tokens: 327
- Bits per token: 2.52
- Tokens per second: 7.57 (encode), 14.10 (decode)
- Attempts used: 2

### Test 2: Chinese message
- Prompt: "请写一段自然、连贯、简短的中文段落，描写傍晚散步时看到的街景。"
- Message: "今晚七点在河边老地方见。带好现金和身份证。"
- Packet length: 151 bytes
- Total tokens: 499
- Bits per token: 2.42
- Tokens per second: 5.84 (encode)
- Attempts used: 4

### Test 3: Very short message
- Prompt: "Write a brief paragraph about cats."
- Message: "Hello world."
- Packet length: 100 bytes
- Total tokens: 315
- Bits per token: 2.54
- Tokens per second: 14.27 (encode)
- Attempts used: 1

### Test 4: Long message
- Prompt: "Write a short story about a person discovering a hidden treasure."
- Message: "The coordinates are 37.7749N, 122.4194W. Meet at the old lighthouse at midnight. Bring the map and the key. Remember: trust no one."
- Packet length: 219 bytes
- Total tokens: 723
- Bits per token: 2.42
- Tokens per second: 10.81 (encode)
- Attempts used: 1

## Key Observations

1. **Round-trip reliability**: All tests successfully recovered the original message
2. **Capacity**: Consistently achieves around 2.4-2.5 bits per token
3. **Bilingual support**: Works well for both English and Chinese
4. **Retry mechanism**: Automatically retries when encountering low-entropy situations
5. **Natural output**: Generated text appears natural and coherent
6. **Header overhead**: The header segment uses about 189-210 tokens for 480 bits (fixed packet bootstrap size)

## Next Steps

Proceed to Milestone 2: Related Work Survey to research LLM steganography and watermarking papers.
