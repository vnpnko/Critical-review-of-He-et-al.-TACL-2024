# A Summary and Discussion of *Exploring Human-Like Translation Strategy with Large Language Models*

**Ivan Pylypenko** · Seminar report, *Models on Text*, Technical University of Munich, 2026

📄 **[Read the report (PDF)](pylypenko-2026-maps-review.pdf)**

---

## About

This report reviews **MAPS** (Multi-Aspect Prompting and Selection), proposed by [He et al. (2024)](https://aclanthology.org/2024.tacl-1.13/) in *Transactions of the Association for Computational Linguistics*. It summarizes the method and experiments, then asks how far MAPS is *genuinely human-like* rather than *human-inspired engineering*.

## What MAPS does

MAPS is an inference-time framework for LLM translation that leaves model weights unchanged:

1. **Prepare.** The LLM generates three kinds of guidance for the source sentence:
   - **Keywords:** important source expressions with proposed target equivalents.
   - **Topic:** a specific description of what the sentence is about.
   - **Demonstration:** a related bilingual example sentence pair.
2. **Generate.** Each type of guidance produces a separate translation candidate, alongside a direct zero-shot translation.
3. **Select.** Quality estimation (e.g. COMET-QE) picks the final output.

According to He et al., across three LLMs and 11 WMT22 translation directions, MAPS outperforms ordinary reranking with an equally sized candidate pool by about **0.7 COMET** on average, and reduces hallucinations by **up to 8%** (vs. 3% for reranking).

## Main arguments of the review

- **Structured diversity is the real contribution.** MAPS beats reranking with the same number of candidates and the same selector. This suggests that *differently conditioned* candidates make a stronger pool than repeated sampling. However, total computation (prompts, tokens, latency) is not matched.
- **Human-like only at a procedural level.** MAPS mirrors recognisable steps of translation practice: preparation, considering alternatives and evaluation. It does not model attention, cognitive effort, or consultation of trusted resources. Translation-process research also suggests human work is more iterative than a three-stage pipeline. Better outputs alone do not establish cognitive equivalence.
- **Guidance types share the same errors.** Keywords, topic and demonstration all come from the same model. They are not independent evidence and can reproduce a shared misconception. Keyword suggestions in particular are followed closely although they are never verified against a terminology resource.
- **Selection is essential but imperfect.** The gap to oracle selection shows that strong candidates are sometimes discarded. MAPS needs selectors that are better calibrated for adequacy errors and hallucination.
- **Limited generalisation evidence.** The experiments are sentence-level, human evaluation covers only English↔Chinese, and the tested systems are an earlier generation of LLMs.

**Conclusion:** MAPS is best understood as a *human-inspired engineering framework* rather than a validated cognitive model. Its broader lesson is that translation benefits from separating interpretation, generating alternatives and making the final decision, rather than treating translation as a single act of generation.

The report proposes the following future directions:

- Trigger MAPS adaptively, only for ambiguous or terminology-heavy sentences.
- Replace generated guidance with *retrieved* terminology, demonstrations and document context.
- Follow selection with targeted refinement or candidate fusion.
- Evaluate under matched compute and cost budgets.

## Report structure

1. Introduction
2. Method: framework overview, guidance and candidate generation, candidate selection
3. Experiments and Results: controlled comparisons, automatic and human results, guidance noise and hallucination, candidate pool and selection
4. Related Work and Comparative Context
5. Discussion: contributions and methodological strengths, limitations and unresolved questions, extent of human-likeness and future directions
6. Conclusion

## Original paper

- Paper: [ACL Anthology](https://aclanthology.org/2024.tacl-1.13/) · [arXiv:2305.04118](https://arxiv.org/abs/2305.04118)
- Official code: [zwhe99/MAPS-mt](https://github.com/zwhe99/MAPS-mt)

## See also

- [Terminology-Constrained Machine Translation for Enterprise Software Documentation](https://github.com/vnpnko/terminology-translation): a related project with Robin Schukrafft and Ilnur Gayetov. It compares *verified* term lists in prompts with LoRA fine-tuning, which is the kind of external terminology grounding this review argues MAPS lacks.

## How to cite

```bibtex
@misc{pylypenko2026maps,
  author       = {Pylypenko, Ivan},
  title        = {A Summary and Discussion of ``Exploring Human-Like Translation Strategy with Large Language Models''},
  howpublished = {Seminar report, Models on Text, Technical University of Munich},
  year         = {2026},
  url          = {https://github.com/vnpnko/Critical-review-of-He-et-al.-TACL-2024}
}

@article{he-etal-2024-exploring,
  author  = {He, Zhiwei and Liang, Tian and Jiao, Wenxiang and Zhang, Zhuosheng and Yang, Yujiu and Wang, Rui and Tu, Zhaopeng and Shi, Shuming and Wang, Xing},
  title   = {Exploring Human-Like Translation Strategy with Large Language Models},
  journal = {Transactions of the Association for Computational Linguistics},
  volume  = {12},
  pages   = {229--246},
  year    = {2024},
  doi     = {10.1162/tacl_a_00642}
}
```

## License

[MIT](LICENSE) © 2026 Ivan Pylypenko
