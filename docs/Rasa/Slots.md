## Slots in Rasa
We can think of Slots as the bot's memory, a way for values to be persistent.

#### When not to use Slots?
Consider the example
```text
Could you add 1223239 and 190239?
```
Here `1223239` and `190239` can be classsified as `operands` with `add` being the `operator`. 
 While we can store them as slots, they're better represented as entities as their use is temporary and often not relevant to the rest of the conversation.

