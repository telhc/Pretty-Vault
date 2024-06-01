---
tags:
  - Coding💻
---
## Attention Block
intersperse communication (multi-headed attention) & computation (feed forward)
```python
class Block(nn.Module):
    """ Transformer block: communication followed by computation """
    def __init__(self, n_embed, n_head):
        # n_embed: embedding dimension, n_head: the number of heads we'd like
        super().__init__()
        head_size = n_embed // n_head
        self.sa = MultiHeadAttention(n_head, head_size)
        self.ffwd = FeedFoward(n_embed)

        # Layer normalization across EMBEDDING dimension (per token features)
        self.ln1 = nn.LayerNorm(n_embed)
        self.ln2 = nn.LayerNorm(n_embed)

    def forward(self, x):
        # residual connection - fork off & come back on residual pathway
        x = x + self.sa(self.ln1(x)) # apply layer norm BEFORE attention
        # residual connection - fork off & come back on residual pathway
        x = x + self.ffwd(self.ln2(x)) # apply layer norm BEFORE feed forward
        return x
```

___
> [!note] References
> [Let's build GPT: from scratch, in code, spelled out.](https://www.youtube.com/watch?v=kCc8FmEb1nY) by Andrej Karpathy [GitHub - karpathy/ng-video-lecture](https://github.com/karpathy/ng-video-lecture)
> [[Attention]]

