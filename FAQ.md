# Frequently Asked Questions

## What libraries can I use with Art Blocks?

Currently Art Blocks supports the following libraries:
+ No Library at all (Vanilla JS, CSS, HTML, WebGL)
+ p5js
+ threejs
+ a-frame
+ vox
+ megavox
+ regl
+ SVG

Additional libraries may be added at moderater discression, but the rule is only one external library per project.

## Can I use [insert library not on list here]?

Maybe? If it is just a single JavaScript file, you may be able to work something out with the admins, but no guarantees.

## I heard I shouldn't use Math.random or p5.random. Why not?

When users mint each piece, they are creating a hash token on the blockchain. All the attributes of your piece should be derived from that token
so that user will be able to render their piece and get the same results each time. `Math.random` and `random` from `p5` are both derived from the
computer's clock, so it will be completely random each time you run the piece. There are a number of options for how to handle this randomness in
this repo's `README.md` file.

## Do I need to know solidity (the Ethereum scripting language)?

No. Art Blocks handles all of that for you. All you need to do is the artwork.

## Is there a maximum size for my application?

Technically not, but the artist is responsible for paying to put the code onto the blockchain. Each project has a reference to the source code stored
on-chain that acts as the permanent source of truth. Storing data on-chain gets *very expensive*, so you'll want to spend some time shrinking your code as 
tiny as possible. Artists have recently targeted between ~5-20k for their code (without the library), but obviously this will vary by project scope. 

## Does the size include the library that I'm using?

No, the library you use is not stored on-chain with your project. The Libary you choose will be injected into the window scope when the project runs.

## Really, how expensive is it to put my code on-chain?

The actual cost can vary a lot with current gas prices, but pretty much follows the formula `675 * Bytes * Gwei Price * (1/1000000000)`. So a 10k project at 100 gwei would be:

```
675 * 10000 * 100 * (1 / 1000000000)
675000000 / 1000000000
0.675 ETH
```

## Can I load external assets into my project (textures, audio, etc)?

Not yet. Some ideas are being worked on that will allow external assets to get pulled in, but currently everything must be included in the script file. For
small and critical assets, you may be able to use `base-64` encoding to encode the asset into your script, but that will count as data to be stored.

## Can I use text? What fonts can I use?

You can use text in your project! Font choice is technically at your discression but you're encouraged to use the core web fonts to ensure universal support and maintain the integrity of the piece over the longer term. 
(`serif`, `sans-serif`, `monospace` and less commonly `cursive` and `fantasy`)

## I heard the output sould be 'resolution agnostic,' what's that all about?

Your project should look basically the same whether it is rendered at 200 x 200 or 20,000 x 20,000. It's obviously not going to be pixel perfect, but
the piece should be visually identical at any resolution. You may, however, add constraints to the aspect ratio as long as the result is still resolution
independent.

## How does my project get those OpenSea properties?

Once your project is selected to be included in one of the Art Blocks collections, the onboarding team will help you with this. The one thing to keep in mind
is that all of the properties you want displayed should be directly generated from the transaction hash and should not depend on any other randomness. Behind
the scenes, a small script is run with each transactions that will publish each piece's propeties onto the piece metadata.

## What does it mean that the code lives on-chain?

At its most basic, the Ethereum network is like a cloud computer where everyone can see the inputs and outputs of any function. Because all the inputs and
outputs are public and verified by a network of random computers, you can have a lot of trust that the computation isn't cheating and is following all of
the expected rules. One consequence of the way this all works is that the entire network will have copies of all the inputs and outputs for every transaction
that each node will need to store indefinitely. Art Blocks leverages this fact by making the code for each project the input to a transaction that saves the code. 
In this way, the code for generating each piece is stored for as long as the network remains active in a whole ton of computers all over the world.
In theory it should be possible to recreate all of these projects very far into the future (so long as JavaScript can be emulated and a reference can be
found to the libraries).

## What is gas and why does everyone keep talking about it?

If we think about the Ethereum network as a computer and transactions as functions, each transaction has a certain amount of computation power that is needed
to run it. The cost for each operation in a transaction is expressed in gas. The more operations in a function or the more complex those operations are, the more
gas it will cost to run that function.

When I decide to run a transaction, that transaction has an idea of how much gas it will take to run and I can decide how much I want to pay for each gas. The
price for each unit of gas is expressed in billionths of an ether or 'gwei'. The higher the gas price I'm willing to pay, the more likely it is that someone will
execute that transaction for me (they get to keep whatever the gas cost is). If I need a transaction done really quickly, I'll probably want to use a pretty high 
gas price. If I don't need it done anytime soon, I could probably get away with paying less.

With Art Blocks drops, we have historically spiked the gas price in a very short period of time. Lots of people all wanted fast transactions all at the same time
since if your transaction was too slow, you would miss out on the drop and lose whatever gas you paid. Sometimes the gas would spike very high, it wan't uncommon to
spend as much on gas as on the art itself! The Art Blocks team has been combating this by offering larger editions and limiting it to one transaction 
per wallet to start. Gas still spikes for various reasons throughout the day, so it's a good idea to keep an eye on prices if you're planning on minting a piece.
