# OPENAI GPT OSS 120B with vLLM

## Provide 2 GPT-OSS-120B API Endpoint

```python
vllm_gpt_oss_120b_1="http://210.61.209.139:45014/v1/"
vllm_gpt_oss_120b_2="http://210.61.209.139:45005/v1/"
```

## Install python package

```baspythonh
pip install requests openai
```

## Initialize OpenAI Client

base_url = vllm_gpt_oss_120b_1 or vllm_gpt_oss_120b_2

```python

from openai import OpenAI
client = OpenAI(
    base_url=base_url,
    api_key="dummy-key"
)
```

## Send a Prompt

### Text Generation Example

```python
# 文字生成測試

message="Once upon a time in a magical forest,"

try:

    response = client.completions.create(
        model=model_name,
        prompt=message,
        max_tokens=100,
        temperature=0.8
    )
        
    generated_text = response.choices[0].text
    print("Prompt:", message)
    print("Generated text:", generated_text)
         
except Exception as e:
    print(f"Error: {e}")
```

### Chat Completion Example

```python
# Chat completion 測試 
try:

    chat_response = client.chat.completions.create(
        model=model_name,
        messages=[
            {"role": "system", "content": "You are a helpful assistant."},
            {"role": "user", "content": "Explain machine learning in one paragraph."}
        ],
        temperature=0.7
    )

    response_content = chat_response.choices[0].message.content
    print("Chat response:", response_content)
          
except Exception as e:
    print(f"Chat error: {e}")
```

### Reasoning Effort Example

```python
# Reasoning Effort 測試 - 複雜推理任務

try:
    
    reasoning_response = client.chat.completions.create(
        model=model_name,
        messages=[
            {"role": "system", "content": "You are an expert problem solver. Think step by step and show your reasoning process."},
            {"role": "user", "content": """
            Solve this logic puzzle step by step:
            
            Three friends - Alice, Bob, and Carol - each have a different pet (cat, dog, bird) and live in different colored houses (red, blue, green).
            
            Clues:
            1. Alice doesn't live in the red house
            2. The person with the cat lives in the blue house
            3. Bob doesn't have a bird
            4. Carol doesn't live in the green house
            5. The person in the red house has a dog
            
            Who has which pet and lives in which house?
            """}
        ],
        temperature=0.1,  # 低溫度確保邏輯一致性
        max_tokens=500
    )
    reasoning_content = reasoning_response.choices[0].message.content
    print("Reasoning Response:", reasoning_content)
    
        
except Exception as e:
    print(f"Reasoning error: {e}")
```

## Reference

- [How to run gpt-oss with vLLM | OpenAI Cookbook](https://cookbook.openai.com/articles/gpt-oss/run-vllm)
- [GPT OSS vLLM Recipes](https://docs.vllm.ai/projects/recipes/en/latest/OpenAI/GPT-OSS.html)
- [gpt-oss-120b and gpt-oss-20b 完整指南](https://www.wbolt.com/tw/gpt-oss.html)
