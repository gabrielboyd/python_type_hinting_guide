
# python_type_hinting_guide

**Modern Python Type Hinting Guide (Python 3.14, working draft)**

This repository contains a working draft of a comprehensive guide to modern Python type hinting, current as of Python 3.14. The guide focuses on *practical usage, design intent, and static-analysis–driven reasoning*, rather than duplicating reference material from the standard documentation.

The document is publicly visible to enable review and discussion. It is shared specifically to collect feedback before being stabilized into a more authoritative version.

## Start here
→ [Read the draft guide](type_hinting_git_v0.1.md)

---

## How to Engage

Comments, issues, and pull requests are welcome. The most valuable feedback at this stage is:

* Conceptual errors or oversights in how typing features are explained
* Corrections or improvements to links and references to official Python documentation, with a preference for consolidated references (e.g. typing module specs) over individual PEPs where possible.
* Inaccuracies or edge cases in checker behavior (mypy, pyright, etc.)
* Places where the explanation is correct but unclear or misleading to non-experts
* Structural or pedagogical suggestions (ordering, grouping, emphasis)
* Missing topics that materially affect real-world typing practice


You should assume the document is *directionally correct but not yet final*. If something seems wrong, ambiguous, or overstated, that is precisely the kind of feedback this draft is meant to surface.

---

## Status and Licensing

This is a public, timestamped draft. It should not yet be treated as authoritative or complete.

The document is **not currently open-licensed**. Redistribution, reuse, or incorporation into other works outside this repository is not permitted without explicit permission from the author. Licensing and attribution terms may change once the document stabilizes.
https://github.com/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#core-annotation-syntax
---
- [Overview of Python Type Hinting (aka typing)](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#overview-of-python-type-hinting-aka-typing)
  * [Preface](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#preface)
  * [Brief Discussion of Type Theory, Type Systems, and Role of Type Hinting](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#brief-discussion-of-type-theory-type-systems-and-role-of-type-hinting)
  * [New Adopters - Where Have You Seen This and Why Does It Matter?](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#new-adopters---where-have-you-seen-this-and-why-does-it-matter)
  * [Typing as Epistemic Resolution and Semantic Fidelity](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#typing-as-epistemic-resolution-and-semantic-fidelity)
  * [General Organization](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#general-organization)
  * [Syntax Parallels Object Declarations](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#syntax-parallels-object-declarations)
  * [Type Hints Require Structural Specificity](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#type-hints-require-structural-specificity)
  * [Related Features](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#related-features)
- [Python's Native Typing Support](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#pythons-native-typing-support)
  * [Standard Typing Support](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#standard-typing-support)
  * [The Modern Standard: Built-in Generics](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#the-modern-standard-built-in-generics)
  * [Core Annotation Syntax](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#core-annotation-syntax)
  * [Type Specificity and Flexibility: Union, Any, and object](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#type-specificity-and-flexibility-union-any-and-object)
- [Tuples: Structured Records vs. Uniform Collections](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#tuples-structured-records-vs-uniform-collections)  
  * [Structured Tuples: Describing a Shape](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#structured-tuples-describing-a-shape)
  * [Variadic Tuples: Describing a Uniform Sequence](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#variadic-tuples-describing-a-uniform-sequence)       
- [Typing Collections](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#typing-collections)
- [Type Inference and Resolution](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#type-inference-and-resolution)
  * [Resolving to a Common Type](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#resolving-to-a-common-type)
  * [Numeric Type Promotion](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#numeric-type-promotion)
  * [Conditional Resolution](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#conditional-resolution)
  * [Advanced Type Narrowing with Custom Guards](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#advanced-type-narrowing-with-custom-guards)
  * [Structural Resolution](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#structural-resolution)
  * [Advanced Narrowing: Promises vs. Proof](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#advanced-narrowing-promises-vs-proof)
- [CRITICAL USE CASE: Typing Data from the Edge](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#critical-use-case-typing-data-from-the-edge)
  * [The Lightweight Solution: `TypedDict`](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#the-lightweight-solution-typeddict)
  * [Handling Optional Keys in `TypedDict`](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#handling-optional-keys-in-typeddict)
  * [The Robust Solution: Parsing into Data Classes](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#the-robust-solution-parsing-into-data-classes)       
  * [When to Use Which](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#when-to-use-which-1)
- [Typing Functions: Synchronous vs. Asynchronous](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#typing-functions-synchronous-vs-asynchronous)
  * [Typing Synchronous Functions and Methods](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#typing-synchronous-functions-and-methods)
  * [Typing Asynchronous Code](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#typing-asynchronous-code)
- [Constraining `TypeVar`: `bound` and Variance](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#constraining-typevar-bound-and-variance)
  * [Establishing Structural Requirements with `bound`](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#establishing-structural-requirements-with-bound)  
  * [Note: Unlike constrained TypeVars, a bound specifies an upper bound on admissible types, rather than a closed, finite set of allowed types.](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#note-unlike-constrained-typevars-a-bound-specifies-an-upper-bound-on-admissible-types-rather-than-a-closed-finite-set-of-allowed-types) 
  * [Defining Relational Behavior with Variance](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#defining-relational-behavior-with-variance)
- [Advanced Generic Callables: Higher-Order Functions](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#advanced-generic-callables-higher-order-functions) 
  * [Basic Interaction of `TypeVar` with `Callable`](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#basic-interaction-of-typevar-with-callable)
  * [Handling a Variable Number of Types](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#handling-a-variable-number-of-types)
  * [Think of it like this: TypeVarTuple collects the concrete types of positionally dependent arguments into a single pack, and Unpack distributes that pack into another generic type, allowing a generic producer and a generic consumer to share the same positional type information.](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#think-of-it-like-this-typevartuple-collects-the-concrete-types-of-positionally-dependent-arguments-into-a-single-pack-and-unpack-distributes-that-pack-into-another-generic-type-allowing-a-generic-producer-and-a-generic-consumer-to-share-the-same-positional-type-information)
  * [Typing Sequences Using the `*` Syntax](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#typing-sequences-using-the--syntax)
- [Advanced Generic Callables: Wrappers](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#advanced-generic-callables-wrappers)
  * [Preserving Signatures with `ParamSpec`](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#preserving-signatures-with-paramspec)
- [Additional Typing Module Functionality](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#additional-typing-module-functionality)
  * [The Specialist's Toolkit: The `typing` Module](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#the-specialists-toolkit-the-typing-module)
  * [Attribute, Value, and Structural Constraints: `Literal`, `Final`,`@final`, and `ClassVar`](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#attribute-value-and-structural-constraints-literal-finalfinal-and-classvar)
- [Appendix 1: Architectural Best Practices: Building Flexible and Robust Code](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#appendix-1-architectural-best-practices-building-flexible-and-robust-code)
  * [Programming to an Interface: The Power of `Protocol`](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#programming-to-an-interface-the-power-of-protocol)
  * [Trust, But Verify: Runtime Type Enforcement](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#trust-but-verify-runtime-type-enforcement)
- [Appendix 2: Anatomy of Type Declarations and Associated Vocabulary](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#appendix-2-anatomy-of-type-declarations-and-associated-vocabulary)
  * [1\. [Variable / Attribute Annotation](https://peps.python.org/pep-0526/)](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#1-variable--attribute-annotationhttpspepspythonorgpep-0526)
  * [2\. Function / Method Annotation](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#2-function--method-annotation)
  * [3\. Generic Type Annotation](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#3-generic-type-annotation)
  * [4\. [Type Alias Declaration](https://peps.python.org/pep-0695/)](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#4-type-alias-declarationhttpspepspythonorgpep-0695)
  * [5\. Variadic Annotations](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#5-variadic-annotations)
- [Appendix 3: The Typing Tools Ecosystem](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#appendix-3-the-typing-tools-ecosystem)
  * [Your IDE: Where Type Checking Happens First](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#your-ide-where-type-checking-happens-first)
  * [Static Type Checkers: Batch Analysis and CI/CD](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#static-type-checkers-batch-analysis-and-cicd)        
  * [Runtime Validation: Enforcing Types When It Matters](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#runtime-validation-enforcing-types-when-it-matters)
  * [Programmatic Type Checking and Automation](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#programmatic-type-checking-and-automation)
  * [Getting Started](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#getting-started)
  * [The Big Picture](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#the-big-picture)
- [Appendix 4: Major Typing Enhancement Proposals (PEPs)](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#appendix-4-major-typing-enhancement-proposals-peps)
  * [Foundational PEPs](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#foundational-peps)
  * [Structural and Value Constraints](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#structural-and-value-constraints)
  * [Syntactic Simplification](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#syntactic-simplification)
  * [Advanced Generics and Callables](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#advanced-generics-and-callables)
  * [Type Narrowing and Method Contracts](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#type-narrowing-and-method-contracts)
- [Glossary of Typing Terminology](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#glossary-of-typing-terminology)
  * [Contravariance](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#contravariance-1)
  * [Covariance](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#covariance-1)
  * [Gradual Typing](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#gradual-typing)
  * [Heterogeneous Collection](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#heterogeneous-collection)
  * [Homogeneous Collection](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#homogeneous-collection)
  * [Insufficiently Typed Operation](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#insufficiently-typed-operation)
  * [Invariance](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#invariance)
  * [Nominal Subtyping](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#nominal-subtyping)
  * [Predicate](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#predicate)
  * [Structural Subtyping](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#structural-subtyping)
  * [Subtyping](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#subtyping)
  * [Sufficiently Typed Operation](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#sufficiently-typed-operation)
  * [Type Ambiguity](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#type-ambiguity)
  * [Type Narrowing](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#type-narrowing)
  * [Union Type](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#union-type)
  * [Variadic](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#variadic)
  * [Variance](/JBogEsq/python_type_hinting_guide/blob/main/type_hinting_git_v0.1.md#variance)
