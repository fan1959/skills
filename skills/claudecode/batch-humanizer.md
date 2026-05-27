---
name: batch-humanizer
description: Batch AI humanization for Chinese documents with multiple iteration rounds
---

# Batch AI Humanizer

Apply multiple rounds of AI humanization to Chinese documents to remove AI writing patterns.

## Workflow

1. **Read source document** - Extract content from .docx file
2. **Apply humanization rounds** (default: 3 rounds, configurable up to 5)
   - Remove AI patterns
   - Check for repetition
   - Verify natural flow
3. **Save output** - Save humanized version as new file

## Usage

```
/batch-humanizer <input-file> [--output <output-file>] [--rounds <1-5>]
```

## Round Details

Each round applies these transformations:

### Round 1-2: Pattern Removal
- Remove "首先、其次、最后"
- Remove "综上所述、由此可见"
- Remove "值得注意的是"
- Remove "从...角度来看"
- Remove repetitive transitional phrases

### Round 3-4: Structure Variation
- Vary sentence openings
- Mix short and long sentences
- Add natural Chinese colloquialisms
- Remove formulaic paragraph structures

### Round 5: Final Polish
- Check rhythm and flow
- Verify authenticity
- Ensure readability

## Example Command

```
claude -p "Apply 5 rounds of AI humanization to document.docx and save as document_humanized.docx. For each round: remove AI patterns, check for repetition, verify natural flow." --allowedTools "Bash,Read,Write,Edit,Skill"
```

## Configuration

- Default rounds: 3
- Max rounds: 5
- Output suffix: `_humanized`

## Integration

This skill works with `/humanizer-zh` for single-pass humanization or as a standalone batch processor for multiple rounds.
