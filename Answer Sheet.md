# MOST SIGNIFICANT BIT

Let's look at a byte of information. `0 0 0 0 0 0 0 0`, This byte houses 8 bits, all of them turned off.<br>
The value of this byte is 0.

Now, let's look at this byte. `0 0 0 0 0 0 1 0`, it might look like the value of this byte is obviously 2. <br>
But is it?

Well, to calculate the value of this byte is simply to take each lit bit and calculate it's power of two using it's index. But how do we know what the index of the bit is? what do we use as a reference?

Intro, the **most significant bit**.

The most significant bit is the bit in a binary number that holds the largest value, meaning the biggest power of two. This bit is usually the left-most, or the first transmitted. We will get to how do we know that in the future. MSB is the reference that we use to know what side to start our bit indexing from.

Let's get back to that supposedly 2 binary number from before. `00000010` if the MSB is the left-most bit, that would represent the largest number 2^7 (128). The right-most bit would represent 2^0 (1) then the bit that is right side to that one will represent 2. However if the right-most bit is the MSB, then the one right side to that will represent one power lower, so that binary number can be interperted as 2^6 which is 64 as well.

It's all depending on the MSB placement.