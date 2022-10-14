# License

## OVOS License

we have a universal donor policy, our code should be able to be used anywhere by anyone, no ifs or conditions attached.

We will always license our code under Apache2, BSD, or as permissive a license as legally possible.

Individual plugins or skills may have their own license, for example mimic3 is AGPL so we can not change the license of
our plugin.

We are committed to maintain all core components fully free, any non-permissive code will live in an optional plugin and be flagged
as such.

This includes avoiding LGPL code for reasons explained [below](#legalese)


## Notable licensing exceptions

The following repositories do not respect our [universal donor policy](#how-is-ovos-licensed), please ensure their
licenses are compatible before you use them

| Repository                                                                                  | License   | Reason                                                                                                     |
|---------------------------------------------------------------------------------------------|-----------|------------------------------------------------------------------------------------------------------------|
| [ovos-intent-plugin-padatious](https://github.com/OpenVoiceOS/ovos-intent-plugin-padatious) | Apache2.0 | [padatious](https://github.com/MycroftAI/padatious) license might not be valid, depends on libfann2 (LGPL) |
| [ovos-tts-plugin-mimic3](https://github.com/OpenVoiceOS/ovos-tts-plugin-mimic3)             | AGPL      | depends on mimic3 (AGPL)                                                                                   |
| [ovos-tts-plugin-SAM](https://github.com/OpenVoiceOS/ovos-tts-plugin-SAM)                   | ?         | reverse engineered abandonware                                                                             |


## Universal Donor Policy 

### Why not GPL ?

The GNU Public License (GPL) was created to be the "antithesis" of the standard proprietary license. 
Any modifications that were made to GPL licensed software required to be given back to the GPL community and any application that used or linked to GPL source code was required to be under the GPL.

The main purpose of the GPL is to disallow incorporation of GPL licensed software into proprietary software.

The GPL and licenses modeled on it impose the restriction that source code must be distributed or made available for all works that are derivatives of the GNU copyrighted code.

If you are a end user feel free to disregard everything we say below, there is absolutely nothing wrong with GPL code for users, GPL gives you maximum freedom as an end-user! Enjoy and consider donating to the software you depend on!

If you actually tinker with software things start to get murky, because users and developers are the same thing, programs become libraries and contradictions arise, in short, a bunch of complicated nerd mumbo jumbo is coming up!

### The missing freedom

According to the rules of GPLv3, if we merely link to a GPLv3 library in our own product, the product MUST be released under a GPLv3 license.

While this may look like a noble strategy, it is a condition that is typically unacceptable for commercial use of software.

There are good foundation principles underlying the GPL. We agree with the power of community development, and we think it's important for a GPL license to require that true modifications be returned to the community. That ensures that the product continues to be advanced as a community development project

If we use 10 lines of GPL code in our 100k lines of code, the whole thing needs to be GPL, that's the GPL virus that Richard Stallman wanted to create and did clearly and cleanly.
But we are missing an essential freedom here, that is the freedom to license our own code the way we want, it needs to also be GPL. Regardless of our license of choice respecting the user freedoms or not

By "Free Software" its proponents are careful to point out that they mean "free as in free speech, not as in free beer". That is not entirely accurate. The freedom they promote is not as free as free speech, because free speech means nothing if you are compelled to say what you do not choose. 

GPL compels you to make your own software available in ways you might not choose. The only truly free speech is speech without any compulsions whatsoever, and the GPL does not grant that right. 

This is where the LGPL comes in, The LGPL was originally an attempt to allow a "library" that wouldn't be viral.
But they still wanted the end user to be able to replace the library on their own, hence the distinction between "static" and "dynamic" linking. The user could swap to a different dynamically linked library, so it wouldn't need to be licensed as GPL. And a static link required the user to be GPL

### Legalese

(L)GPL was written with C/C++ in mind, unfortunately. It speaks of "Source Code", "Object Code", "Dynamic Linking", "Static Linking", "Compilers" and "Object Code Interpreter". 
So translating this for other languages that don't follow the same compilation techniques (such as Java's bytecode, Python's just in time compilation or Javascript's interpreted nature) requires some guessing and assumptions.

The license actually talks about "header files", which are clear in C/C++ but obviously not clear when you are in the Java, Python, Javascript, etc. worlds. 
So the L ("library") of LGPL stuff is muddy, at best.

This gets to the crux of the matter. Anything unclear is BAD in the world of laws.

If we're looking at building something using either GPL or LGPL component, we want to be certain what our legal standing is in the future if we land in court. As of today, 
We're not certain because there really haven't been good court cases establishing legal precedent, only intellectual arguments.

From a business perspective, We understand why some don't want to touch GPL code. 
The legal standing is unclear and the business might be stung a decade down the road when legal precedent is finally set. 
Or they might be stuck in court for years fighting to establishing the legal precedent. 
Regardless they just don't want to risk the cost of that battle.

### Permissive licenses

GPL restrictions sometimes put a company in a sore spot. Instead of releasing source code they try to influence the upstream project by hiring one or more of the developers, and then try to effect the project to make changes upstream that helps the company implement whatever solutions they require.

With a permissive license the company can do whatever they want. The situation never arises in which it becomes a part of their interest to "hijack" the upstream project or directly influence the way it is going.

On the contrary, companies who benefit from the permissive license often contribute code back to the project because it is in their interest to have their contributions available in the source code, while at the same time they keep "specific company related" changes private.

Since permissive licenses do not come with the legal complexity of the GPL licenses, it allows developers and companies to spend their time creating and promoting good code rather than worrying if that code violates licensing.

In contrast to the GPL, which is designed to prevent the proprietary commercialization of Open Source code, permissive licenses place minimal restrictions on future behavior. This allows code to remain Open Source or become integrated into commercial solutions, as a project’s or company’s needs change. In other words, permissive licenses do not become a legal time-bomb at any point in the development process.

If a product is licensed with a permissive license, derivative works can be licensed under the GPL, this is what makes a license GPL compatible, but in this case the original product can not take the improvements the GPL version made, because GPL itself is not {permissive-license} compatible.
This relationship between GPL downstream <-> Permissive upstream is parasitic in nature, in practice, using GPL usually ends up hindering free sharing and reuse of code and ideas rather than encouraging it.

We don't believe that you can encourage freedom and sharing by enforcing nonfreedom, it is a double standard no matter how you look at it.

The LGPL is almost there! But since it was written with software of the past decade in mind it might not be safe to use in languages like python. Some people argue LGPL is compatible, but until the matter is settled in court it will at very least hurt adoption

### Final comments

When people use the GPL they mostly try to prevent some corporate entity from taking their software, make improvements or changes to it, and then sell that software as a proprietary product.

But what is it that we're trying to accomplish? Is it competition by proprietary software? Is it to prevent people from making money by developing software and getting food on the table?

We understand the historical background and why the GPL was made and we truly and deeply respect the reasons behind the GPL. 

And it's not that we believe that the GPL is evil, it's just that we don't believe it is achieving the goals today which it was set out to achieve. 

**Not sharing is actually the root of the problem**

By sharing and helping we encourage good behavior and good relations and if only a majority of us keep doing that, at one point "being evil" will not pay off

Companies like Facebook will do evil no matter what.
They will make their own software no matter what. 
Preventing them from using your specific software doesn't change anything and it actually often does more damage than good. 

# Credits

this text is not a 100% original creation, it was adapted from the links below. Huge chunks have been copied verbatim and others slightly altered. 

The full text above reflects our own opinion only and should not be misconstrued as representing the opinion of the authors of the articles below. 
We repeat, those people don't even know this text exists, they do not approve the editorial changes and additions we made

- https://softwareengineering.stackexchange.com/questions/119436/what-does-gpl-with-classpath-exception-mean-in-practice/326325#326325
- https://unixsheikh.com/articles/the-problems-with-the-gpl.html
- https://docs.freebsd.org/en/articles/bsdl-gpl/