When a blockchain has multiple branches, also called "tips of the chain", and is not sure yet which one is the correct one.  

```mermaid
graph TD
	direction LR
    A --> B --> C --> D0?
    C --> D1?
```

These concurrent tips need to be eventually resolved into one. The correct fork is called the **canonical chain**.