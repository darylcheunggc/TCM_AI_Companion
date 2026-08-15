## 2026-8-14
- Discovered SymMap has no entry for floater - 飞蚊症 - turns out it's indexed under the classical term 云雾移睛. Real lesson: Need a synonym-mapping layer before RAG can handle modern-term queries against classical sources.
Confirmed GB10 100% Ollama/GGUF today. No NVFP4/NIM/vLLM. Explains the slowness. Plan: pull beg-m3 + deepseek-r1 32b, then try vLLM.
- Plan for RAG using bge-m3 for embedding and deepseek-r1:32b to replace 70B
- Install vLLM via Nvidia's official DGX Spark Guide and re-test Qwen 2.5-14B to unlock real speed on this. Need to re-run speed comparison.
-----------------------------------------------------------------------------------------------------------------------------------------------
ADDITIONAL NOTE TO SELF
- Each phase checkpoint --> Turn Relevant DEVLOP entires into short clean write up 
  A) What I've built
  B) What problems it solves,
  C) What I've learned
  D) Provide GitHub Link to Manager with polished write-up team message with link attached (Mile-stone summaries)
-------------------------------------------------------------------------------------------------------------------------------------------------
## 2026-8-15
- Testing commit changes and how it will be shown.
