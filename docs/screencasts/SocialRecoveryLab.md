# Screencast: Managing Your Recovery Key Through Sharding 

In this screencast, we demonstrate how you might go about “sharding” your recovery key and distributing it amongst several holders, as well as how you would go about restoring the key from those shards. Remember, social recovery is an approach to the dilemma of wanting convenient, online storage of your key, without the risk of a remote attack. The process involves sharding or splitting the key into pieces and distributing the pieces amongst a set of holders. The sharding process (called "[Shamir’s Secret Sharing](https://en.wikipedia.org/wiki/Shamir%27s_Secret_Sharing)"—the math is really neat!) is done such that a subset (for example, any three out of five) of the pieces can be combined to restore the entire key.

To illustrate Shamir’s Secret Sharing, we use a website called [PassGuardian.com](http://passguardian.com/)that was created to demonstrate an implementation of secret sharing. Feel free to try out [PassGuardian.com](http://passguardian.com/) yourself once you’ve listened to the lab.

To start the lab, click [here](https://youtu.be/1c05mFuEQ5s).
