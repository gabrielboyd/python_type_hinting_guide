
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

---

- [Overview of Python Type Hinting (aka typing)](./blob/main/type_hinting_git_v0.1.md#overview-of-python-type-hinting-aka-typing)
  * [Preface](./blob/main/type_hinting_git_v0.1.md#preface)
  * [Brief Discussion of Type Theory, Type Systems, and Role of Type Hinting](./blob/main/type_hinting_git_v0.1.md#brief-discussion-of-type-theory-type-systems-and-role-of-type-hinting)
  * [New Adopters - Where Have You Seen This and Why Does It Matter?](./blob/main/type_hinting_git_v0.1.md#new-adopters---where-have-you-seen-this-and-why-does-it-matter)      
  * [Typing as Epistemic Resolution and Semantic Fidelity](./blob/main/type_hinting_git_v0.1.md#typing-as-epistemic-resolution-and-semantic-fidelity)
  * [General Organization](./blob/main/type_hinting_git_v0.1.md#general-organization)   
  * [Syntax Parallels Object Declarations](./blob/main/type_hinting_git_v0.1.md#syntax-parallels-object-declarations)
  * [Type Hints Require Structural Specificity](./blob/main/type_hinting_git_v0.1.md#type-hints-require-structural-specificity)
  * [Related Features](./blob/main/type_hinting_git_v0.1.md#related-features)
- [Python's Native Typing Support](./blob/main/type_hinting_git_v0.1.md#pythons-native-typing-support)
  * [Standard Typing Support](./blob/main/type_hinting_git_v0.1.md#standard-typing-support)
  * [The Modern Standard: Built-in Generics](./blob/main/type_hinting_git_v0.1.md#the-modern-standard-built-in-generics)
  * [Core Annotation Syntax](./blob/main/type_hinting_git_v0.1.md#core-annotation-syntax)
  * [Type Specificity and Flexibility: Union, Any, and object](./blob/main/type_hinting_git_v0.1.md#type-specificity-and-flexibility-union-any-and-object)
- [Tuples: Structured Records vs. Uniform Collections](./blob/main/type_hinting_git_v0.1.md#tuples-structured-records-vs-uniform-collections)
  * [Structured Tuples: Describing a Shape](./blob/main/type_hinting_git_v0.1.md#structured-tuples-describing-a-shape)
  * [Variadic Tuples: Describing a Uniform Sequence](./blob/main/type_hinting_git_v0.1.md#variadic-tuples-describing-a-uniform-sequence)
- [Typing Collections](./blob/main/type_hinting_git_v0.1.md#typing-collections)
- [Type Inference and Resolution](./blob/main/type_hinting_git_v0.1.md#type-inference-and-resolution)
  * [Resolving to a Common Type](./blob/main/type_hinting_git_v0.1.md#resolving-to-a-common-type)
  * [Numeric Type Promotion](./blob/main/type_hinting_git_v0.1.md#numeric-type-promotion)
  * [Conditional Resolution](./blob/main/type_hinting_git_v0.1.md#conditional-resolution)
  * [Advanced Type Narrowing with Custom Guards](./blob/main/type_hinting_git_v0.1.md#advanced-type-narrowing-with-custom-guards)
  * [Structural Resolution](./blob/main/type_hinting_git_v0.1.md#structural-resolution) 
  * [Advanced Narrowing: Promises vs. Proof](./blob/main/type_hinting_git_v0.1.md#advanced-narrowing-promises-vs-proof)
- [CRITICAL USE CASE: Typing Data from the Edge](./blob/main/type_hinting_git_v0.1.md#critical-use-case-typing-data-from-the-edge)
  * [The Lightweight Solution: `TypedDict`](./blob/main/type_hinting_git_v0.1.md#the-lightweight-solution-typeddict)
  * [Handling Optional Keys in `TypedDict`](./blob/main/type_hinting_git_v0.1.md#handling-optional-keys-in-typeddict)
  * [The Robust Solution: Parsing into Data Classes](./blob/main/type_hinting_git_v0.1.md#the-robust-solution-parsing-into-data-classes)
  * [When to Use Which](./blob/main/type_hinting_git_v0.1.md#when-to-use-which-1)       
- [Typing Functions: Synchronous vs. Asynchronous](./blob/main/type_hinting_git_v0.1.md#typing-functions-synchronous-vs-asynchronous)
  * [Typing Synchronous Functions and Methods](./blob/main/type_hinting_git_v0.1.md#typing-synchronous-functions-and-methods)
  * [Typing Asynchronous Code](./blob/main/type_hinting_git_v0.1.md#typing-asynchronous-code)
- [Constraining `TypeVar`: `bound` and Variance](./blob/main/type_hinting_git_v0.1.md#constraining-typevar-bound-and-variance)
  * [Establishing Structural Requirements with `bound`](./blob/main/type_hinting_git_v0.1.md#establishing-structural-requirements-with-bound)
  * [Note: Unlike constrained TypeVars, a bound specifies an upper bound on admissible types, rather than a closed, finite set of allowed types.](./blob/main/type_hinting_git_v0.1.md#note-unlike-constrained-typevars-a-bound-specifies-an-upper-bound-on-admissible-types-rather-than-a-closed-finite-set-of-allowed-types)
  * [Defining Relational Behavior with Variance](./blob/main/type_hinting_git_v0.1.md#defining-relational-behavior-with-variance)
- [Advanced Generic Callables: Higher-Order Functions](./blob/main/type_hinting_git_v0.1.md#advanced-generic-callables-higher-order-functions)
  * [Basic Interaction of `TypeVar` with `Callable`](./blob/main/type_hinting_git_v0.1.md#basic-interaction-of-typevar-with-callable)
  * [Handling a Variable Number of Types](./blob/main/type_hinting_git_v0.1.md#handling-a-variable-number-of-types)
  * [Think of it like this: TypeVarTuple collects the concrete types of positionally dependent arguments into a single pack, and Unpack distributes that pack into another generic type, allowing a generic producer and a generic consumer to share the same positional type information.](./blob/main/type_hinting_git_v0.1.md#think-of-it-like-this-typevartuple-collects-the-concrete-types-of-positionally-dependent-arguments-into-a-single-pack-and-unpack-distributes-that-pack-into-another-generic-type-allowing-a-generic-producer-and-a-generic-consumer-to-share-the-same-positional-type-information)
  * [Typing Sequences Using the `*` Syntax](./blob/main/type_hinting_git_v0.1.md#typing-sequences-using-the--syntax)
- [Advanced Generic Callables: Wrappers](./blob/main/type_hinting_git_v0.1.md#advanced-generic-callables-wrappers)
  * [Preserving Signatures with `ParamSpec`](./blob/main/type_hinting_git_v0.1.md#preserving-signatures-with-paramspec)
- [Additional Typing Module Functionality](./blob/main/type_hinting_git_v0.1.md#additional-typing-module-functionality)
  * [The Specialist's Toolkit: The `typing` Module](./blob/main/type_hinting_git_v0.1.md#the-specialists-toolkit-the-typing-module)
  * [Attribute, Value, and Structural Constraints: `Literal`, `Final`,`@final`, and `ClassVar`](./blob/main/type_hinting_git_v0.1.md#attribute-value-and-structural-constraints-literal-finalfinal-and-classvar)
- [Appendix 1: Architectural Best Practices: Building Flexible and Robust Code](./blob/main/type_hinting_git_v0.1.md#appendix-1-architectural-best-practices-building-flexible-and-robust-code)
  * [Programming to an Interface: The Power of `Protocol`](./blob/main/type_hinting_git_v0.1.md#programming-to-an-interface-the-power-of-protocol)
  * [Trust, But Verify: Runtime Type Enforcement](./blob/main/type_hinting_git_v0.1.md#trust-but-verify-runtime-type-enforcement)
- [Appendix 2: Anatomy of Type Declarations and Associated Vocabulary](./blob/main/type_hinting_git_v0.1.md#appendix-2-anatomy-of-type-declarations-and-associated-vocabulary)  
  * [1\. [Variable / Attribute Annotation](https://peps.python.org/pep-0526/)](./blob/main/type_hinting_git_v0.1.md#1-variable--attribute-annotationhttpspepspythonorgpep-0526) 
  * [2\. Function / Method Annotation](./blob/main/type_hinting_git_v0.1.md#2-function--method-annotation)
  * [3\. Generic Type Annotation](./blob/main/type_hinting_git_v0.1.md#3-generic-type-annotation)
  * [4\. [Type Alias Declaration](https://peps.python.org/pep-0695/)](./blob/main/type_hinting_git_v0.1.md#4-type-alias-declarationhttpspepspythonorgpep-0695)
  * [5\. Variadic Annotations](./blob/main/type_hinting_git_v0.1.md#5-variadic-annotations)
- [Appendix 3: The Typing Tools Ecosystem](./blob/main/type_hinting_git_v0.1.md#appendix-3-the-typing-tools-ecosystem)
  * [Your IDE: Where Type Checking Happens First](./blob/main/type_hinting_git_v0.1.md#your-ide-where-type-checking-happens-first)
  * [Static Type Checkers: Batch Analysis and CI/CD](./blob/main/type_hinting_git_v0.1.md#static-type-checkers-batch-analysis-and-cicd)
  * [Runtime Validation: Enforcing Types When It Matters](./blob/main/type_hinting_git_v0.1.md#runtime-validation-enforcing-types-when-it-matters)
  * [Programmatic Type Checking and Automation](./blob/main/type_hinting_git_v0.1.md#programmatic-type-checking-and-automation)
  * [Getting Started](./blob/main/type_hinting_git_v0.1.md#getting-started)
  * [The Big Picture](./blob/main/type_hinting_git_v0.1.md#the-big-picture)
- [Appendix 4: Major Typing Enhancement Proposals (PEPs)](./blob/main/type_hinting_git_v0.1.md#appendix-4-major-typing-enhancement-proposals-peps)
  * [Foundational PEPs](./blob/main/type_hinting_git_v0.1.md#foundational-peps)
  * [Structural and Value Constraints](./blob/main/type_hinting_git_v0.1.md#structural-and-value-constraints)
  * [Syntactic Simplification](./blob/main/type_hinting_git_v0.1.md#syntactic-simplification)
  * [Advanced Generics and Callables](./blob/main/type_hinting_git_v0.1.md#advanced-generics-and-callables)
  * [Type Narrowing and Method Contracts](./blob/main/type_hinting_git_v0.1.md#type-narrowing-and-method-contracts)
- [Glossary of Typing Terminology](./blob/main/type_hinting_git_v0.1.md#glossary-of-typing-terminology)
  * [Contravariance](./blob/main/type_hinting_git_v0.1.md#contravariance-1)
  * [Covariance](./blob/main/type_hinting_git_v0.1.md#covariance-1)
  * [Gradual Typing](./blob/main/type_hinting_git_v0.1.md#gradual-typing)
  * [Heterogeneous Collection](./blob/main/type_hinting_git_v0.1.md#heterogeneous-collection)
  * [Homogeneous Collection](./blob/main/type_hinting_git_v0.1.md#homogeneous-collection)
  * [Insufficiently Typed Operation](./blob/main/type_hinting_git_v0.1.md#insufficiently-typed-operation)
  * [Invariance](./blob/main/type_hinting_git_v0.1.md#invariance)
  * [Nominal Subtyping](./blob/main/type_hinting_git_v0.1.md#nominal-subtyping)
  * [Predicate](./blob/main/type_hinting_git_v0.1.md#predicate)
  * [Structural Subtyping](./blob/main/type_hinting_git_v0.1.md#structural-subtyping)   
  * [Subtyping](./blob/main/type_hinting_git_v0.1.md#subtyping)
  * [Sufficiently Typed Operation](./blob/main/type_hinting_git_v0.1.md#sufficiently-typed-operation)
  * [Type Ambiguity](./blob/main/type_hinting_git_v0.1.md#type-ambiguity)
  * [Type Narrowing](./blob/main/type_hinting_git_v0.1.md#type-narrowing)
  * [Union Type](./blob/main/type_hinting_git_v0.1.md#union-type)
  * [Variadic](./blob/main/type_hinting_git_v0.1.md#variadic)
  * [Variance](./blob/main/type_hinting_git_v0.1.md#variance)
