---
layout: single
classes: wide
author_profile: false
sidebar:
  nav: "foo"
header:
  overlay_image: /assets/images/mm-home-page-feature.jpg
title: "Edge Case: Nested and Mixed Lists"
categories:
  - Genomics
tags:
  - content
  - css
  - edge case
  - lists
  - markup
---

Nested and mixed lists are an interesting beast. It's a corner case to make sure that

This post has the date disabled. The date this post was published should not be showing if `show_date: false` is set in `_config.yml` or in this post's YAML Front Matter.

If you could keep awake (but of course you can't) you would see your own mother doing this, and you would find it very interesting to watch her. It is quite like tidying up drawers. You would see her on her knees, I expect, lingering humorously over some of your contents, wondering where on earth you had picked this thing up, making discoveries sweet and not so sweet, pressing this to her cheek as if it were as nice as a kitten, and hurriedly stowing that out of sight. When you wake in the morning, the naughtiness and evil passions with which you went to bed have been folded up small and placed at the bottom of your mind and on the top, beautifully aired, are spread out your prettier thoughts, ready for you to put on.

![image-center](/assets/images/mm-home-page-feature.jpg){: .align-center}

```python

def validate(model, validation_loader,device):
    model.eval()
    correct=0
    with torch.no_grad():
        for data,labels in validation_loader:
            data,labels=data.to(device,dtype=torch.float32), labels.to(device,dtype=torch.float32)
            y_hat=model(data)
            _,y_pred=torch.max(y_hat,1)
            correct+=(y_pred==labels).sum().item()
            #print("f1_score:", f1_score(labels.cpu().data,y_pred.cpu()))
        print("\n Test Set: Average loss: xx , Accuracy:{}/{} ({:.0f}%, f1_score:{})".format(
            correct,len(validation_data),100.*correct/len(validation_data),f1_score(labels.cpu().data,y_pred.cpu())))
        print("="*50)
```

I don't know whether you have ever seen a map of a person's mind. Doctors sometimes draw maps of other parts of you, and your own map can become intensely interesting, but catch them trying to draw a map of a child's mind, which is not only confused, but keeps going round all the time. There are zigzag lines on it, just like your temperature on a card, and these are probably roads in the island, for the Neverland is always more or less an island, with astonishing splashes of colour here and there, and coral reefs and rakish-looking craft in the offing, and savages and lonely lairs, and gnomes who are mostly tailors, and caves through which a river runs, and princes with six elder brothers, and a hut fast going to decay, and one very small old lady with a hooked nose. It would be an easy map if that were all, but there is also first day at school, religion, fathers, the round pond, needle-work, murders, hangings, verbs that take the dative, chocolate pudding day, getting into braces, say ninety-nine, three-pence for pulling out your tooth yourself, and so on, and either these are part of the island or they are another map showing through, and it is all rather confusing, especially as nothing will stand still.

Of course the Neverlands vary a good deal. John's, for instance, had a lagoon with flamingoes flying over it at which John was shooting, while Michael, who was very small, had a flamingo with lagoons flying over it. John lived in a boat turned upside down on the sands, Michael in a wigwam, Wendy in a house of leaves deftly sewn together. John had no friends, Michael had friends at night, Wendy had a pet wolf forsaken by its parents, but on the whole the Neverlands have a family resemblance, and if they stood still in a row you could say of them that they have each other's nose, and so forth. On these magic shores children at play are for ever beaching their coracles [simple boat]. We too have been there; we can still hear the sound of the surf, though we shall land no more.

Of all delectable islands the Neverland is the snuggest and most compact, not large and sprawly, you know, with tedious distances between one adventure and another, but nicely crammed. When you play at it by day with the chairs and table-cloth, it is not in the least alarming, but in the two minutes before you go to sleep it becomes very real. That is why there are night-lights.

Occasionally in her travels through her children's minds Mrs. Darling found things she could not understand, and of these quite the most perplexing was the word Peter. She knew of no Peter, and yet he was here and there in John and Michael's minds, while Wendy's began to be scrawled all over with him. The name stood out in bolder letters than any of the other words, and as Mrs. Darling gazed she felt that it had an oddly cocky appearance.

* Lists within lists do not break the ordered list numbering order
* Your list styles go deep enough.
### `layout: categories`
### Ordered -- Unordered -- Ordered

1. ordered item
2. ordered item 
   * **unordered**
   * **unordered** 
     1. ordered item
     2. ordered item
3. ordered item
4. ordered item

### Ordered -- Unordered -- Unordered

1. ordered item
2. ordered item 
   * **unordered**
   * **unordered** 
     * unordered item
     * unordered item
3. ordered item
4. ordered item

### Unordered -- Ordered -- Unordered

* unordered item
* unordered item 
  1. ordered
  2. ordered 
     * unordered item
     * unordered item
* unordered item
* unordered item

### Unordered -- Unordered -- Ordered

* unordered item
* unordered item 
  * unordered
  * unordered 
    1. **ordered item**
    2. **ordered item**
* unordered item
* unordered item

### Task Lists

- [x] Finish my changes
- [ ] Push my commits to GitHub
- [ ] Open a pull request