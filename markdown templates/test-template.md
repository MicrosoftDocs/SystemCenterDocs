---
# IMPORTANT:
# Ensure you have at least one space after the colon (:) when you provide value(s) for a metadata below
# Your meta data value can NOT have a colon(:). If you must have a colon in your metadata value, please use "" to enclose your metadata value.
# Remove the comment prefix (#) from the optional metadata name when you add a non-empty value to it.

# required metadata

title: ""
author: "Jim-Parker"      # your github alias
ms.author: "jimpark"   # your MSFT alias
manager: ""     # your manager's  MSFT alias
ms.date: ""
ms.topic: ""
ms.prod: ""    # if you use ms.prod, don't use ms.service.
ms.service: "" # if you use ms.service, don't use ms.prod
ms.technology: "" # don't use it for content on Azure.com.
ms.assetid: ""
description: ""
# customer intent: "This article is written for PMs who want to understand how to submit a System Center article that meets the quality review criteria for new TechNet content, so they can write an effective article that will meet the requirements for merge."

---


# Writing technical documentation for CSI

There are as many different ways to write, as there are writers. However, to be consistent, Microsoft requires a particular style and voice that you should understand to write effective technical documentation that will meet our customer's needs and expectations.

In CSI, we start from the perspective that the customer has a job to do and they're reading our content to help them get that job done. As the author, you have a job to do too. It's to serve the reader's immediate need by making it as easy as possible for them do their job. We do this by using an approach called MS Voice.

It doesn't matter whether you're writing content for Azure Backup, Enterprise Mobility, or System Center Operations Manager, that same approach applies. It applies whether you're writing for IT Pros or developers, as well.

This article provides an overview of the MS Voice principles and some introductory guidance for applying them to your writing.

## The MS Voice principles
You can think of voice as a way to remove the hurdles between our customers and the information that we have to offer.

Here are some typical hurdles from the reader’s point of view:

- Dense paragraphs with lots of words.
- Too many details, notes, and exceptions.
- Too much conceptual information getting in the way.
- Too many alternatives.
- Language is formal or technical when it doesn’t need to be.

It is rare for an article to have all of these hurdles, but most articles have some of them.

To address these, and other obstacles, we use 5 Voice principles when writing technical content. They are:

- Focus on the customer intent
- Use everyday words
- Write concisely
- Make it easy to scan
- Show empathy

While you won't apply these principles sequentially, there is a certain "flow" involved in that understanding your customer's intent will help you use the correct words, and using the correct words will help make your content more concise. That flow follows through to the extent that an article addressing the customer's intent, using the right works, written concisely, and made easy to scan naturally shows empathy for the customer's need and helps them do their job quickly and correctly.

## Focus on the customer intent
The single most important MS Voice principle is to focus on the customer intent. The key to identifying the intent is to determine the most common question the customer has and then make the answer ridiculously easy to find. If you haven’t identified your customer and what information they need before you begin, then you’re writing for you, not them.

Ideally, an article has a single customer intent. The intent is the thing the reader wants to do, the task they want to complete. We want to create content that makes it as easy as possible for the reader to find and understand the help they need for this task.

> [!IMPORTANT]
> When we say intent, we always mean **customer intent**. We never mean the author's intent, or the article's intent, or anything else. The author only has one intent, and that's to help the customer get the their job done as efficiently and effectively as possible. And, articles don't have intents.

So, who is your customer, and what is it that they want to do?

### Fill in the blanks
One way to begin identifying the customer intent is to complete the missing parts of the following statement.

As a(n) {customer role}, I need {what information?}, so that I can {do what job?}

For example, As an IT Administrator, I need...

### Some things to ask yourself about customer intent

- What does the customer really want from this article?
- What would a customer type into a search box that should take them directly to this article?

## Use everyday words

The right article is easiest for the customer to find when it uses the right words.

### Word choice

Some people think voice is just about word choice. Word choice is an important part of voice, but it isn’t all of voice.

Some people are also concerned that the Voice initiative is going to force them to write in a way that sounds unprofessional. No one is telling you to say “dude” and “sad panda”. But look for ways to sound less formal. We want to be professional, but not stuffy or robotic.

### Technical words

Another common misconception has to do with technical content. No one is telling you to dumb down your technical content. If your topic is about circular reference errors, you are going to say “circular reference”. If your topic is about domains, you are going to use terms like “DNS record” and “MX record”. Keep those words because they are the right words. But look for other words that might be unnecessarily technical or formal.

To be less formal, not less technical.

Imagine you’re talking to a peer.

### Using the right words

Since word choice differs based on context, you’ll have to use your judgment for what sounds right. People find that it is helpful to look at search keywords to see which words customers are using. .

The right words differ by:
- Audience
- Product
- Feature

You find them by:
- Looking at search keywords
- Reading your content out loud
- Asking other people what they think

It is also extremely helpful to read your content out loud and to ask other people what they think.

### Some things to ask yourself about everyday words

- Does the article use keywords in the title, description, and section headers?
- Does the article sound too formal?
- Does the article use natural language (not cute or casual language)?
- Does the article use words that your audience uses?

## Write concisely

Customers aren’t looking for **more** information; they are looking for the **right** information.

In the past, we’ve erred on the side of being complete–
- every edge case,
- every option,
- every detail,
- every nuance,
- everything we know about the feature in one place.

Err on the side of being concise instead.

When you know what the customer intent is, it is much easier to decide which information is essential and which information is “extra”. Many of our current articles cover several intents. However, if you have data showing you which intents people are looking for, you can split different intents into different articles and put emphasis on the most common tasks.

When you write concisely, there are fewer words getting between your reader and the answer they are looking for.

### Techniques for writing concisely

| Technique | Description |
| --------- | ----------- |
| Use everyday words | See above. |
| Use locators (>) for “click, click, click” instructions | This helps to condense procedure steps. |
| Don’t repeat words that are in the UI | If you are describing the UI, and the UI already has descriptions in it, you likely won’t need to repeat the words. |
| Read out loud | If you are reading out loud and run out of breath, consider paring down that section. |
| Consider using art | Don’t use art for art’s sake, but if art helps you make your point faster, consider it. |
| Delete words that aren’t essential | This technique is the most powerful, and also the most intimidating. It’s hard to delete our beautiful words - and how do you decide what is or isn’t important? |

## Possible deletions
- Conceptual information, if the reader is looking for a procedure
- Edge cases (frequently seen in a proliferation of notes)
- Information that exists in other content (link to it)
- Words that are also in the UI
- Details about something that most people understand
- A separate intent

### Some things to ask yourself about writing concisely

- Have you documented only what is necessary to achieve the intent? Use intent data to suggest what you can delete or move elsewhere.
- How does the article sound when you read out loud?
- Have you deleted all words that aren’t essential?

## Easy to scan
It is easier to scan an article that covers one intent versus an article that covers several.

Move away from the idea of writing everything you know about a topic. Think instead of guiding the reader towards the information they need. Organize your topic in a way that it is easy to navigate. You want to be able to scan for an answer, then read the details when you know you are in the right place.

Sometimes it is useful to organize a topic so that the 80% case is right at the top. The less common cases would then go to the bottom of the article. This might mean that a procedure is put at the top, and conceptual information at the bottom. Or it could mean that notes are pulled out of a procedure and moved into a “tips and troubleshooting” section below the procedure. In a conceptual article, the sections might be organized so that the ones that affect the most people are first.

### Techniques
What are some of the techniques we can use when we want to make an article easy to scan?

| Technique | Description |
| --------- | ----------- |
| Write concisely | When you write concisely, there are fewer words getting between your reader and the answer they are looking for. |
| Put the most important thing first |  |
| Use art | Art really jumps out when used well. If you want to draw attention to something, consider using art. |
| Use tables, lists, and bolding | There are some cases when a paragraph isn’t the best way to present your words. Consider using tables, lists, and bolding to make important parts stand out. |
| Put your section headers to work | Section headers are the unsung champion of an article. If you choose them well, you can help someone navigate through your content, even in a long article. Remember to put search keywords (everyday language!) in your section headers, so that people can find the parts they care about faster. |
| Take the birds’-eye view | “Take the birds’-eye view” is like “read out loud”, but for the visual aspects of an article. Most customers don’t read our articles from the first word to the last. Instead, they scan. To take a step back, print out your article or change the zoom in Word. What does the article look like to someone who hasn’t seen it before? |

### Scannability and SEO
Luckily, search engines are designed to mimic how people scan documents. If an article is easy for a person to scan, then it also likely that a search engine will benefit. This section covers only the way we write to make things easy to scan, but you should talk to your local intent analyst and SEO expert for advice on search tuning.

| Scanned by a person | Scanned by a search engine |
| --------- | ----------- |
| - Title<br /><br /> - Description & introduction<br /><br /> - Section headers<br /><br /> - Art<br /><br /> - Tables, lists, procedures<br /><br /> - Link text<br /><br /> - Body text |
| Title<br /><br /> - Description & introduction<br /><br /> - Section headers<br /><br /> - Art (via alt text)<br /><br /> - Table headers<br /><br /> - Link text<br /><br /> - Body text |



### Some things to ask yourself about scannability

- Is the article too long to allow for scanning? (research tells us that users scan first to determine if the article is what they want)
- Are the most important things first in the article?
- Is the article’s main intent is impossible to miss?
- Does the title and description tell me I’m in the right place?
- Do the section headers lead me through the article?
- Is there any unnecessary information getting in my way?
- Is the article organized so I can find my answer?
- Does the article use art to help scannability?
- Does the article use tables, lists, and bolding?
- Do section headers help the customer achieve their intent? Take the birds’-eye view

## Show empathy
What does empathy look like? It varies per team and per situation, but here are some ways to think of empathy.

| Technique | Description |
| --------- | ----------- |
| Be a partner, not a judge | Empathy can be showing the reader that you are there to help them. |
| Talk like you are helping a coworker | Empathy can be word choice. Talking to the reader like a peer, instead of talking down to them. |
| Don’t imply the problem is their fault | Empathy can be taking responsibility for a problem, or at least not blaming the customer for whatever situation they are in. |
| If the situation is genuinely frustrating, acknowledge it | Empathy can be overt. In some situations, it may be appropriate to say that we are sorry or that many people find something difficult. |
| You don’t have to be their buddy, but don’t be a jerk | Sometimes, in the past, we’ve phrased things in ways that could be misinterpreted. Empathy can be removing those kinds of phrases, and sounding neutral instead. |
| Leave disclaimers to the lawyers | Finally, avoid legal-ese. If you must add a disclaimer because LCA told you to, that is one thing. But for the rest of the article, use a more natural tone. |

Sometimes empathy is just solving the right problem. If the reader has a problem, and you give them the answer that they can understand, that can be perceived as empathy. If you know what your customer cares about, show that.

Sometimes empathy can be acknowledging that our readers aren’t all coming from the same place. This can mean giving background information for beginners, giving instructions that apply to different devices and input methods, or in doing a voice over for a video that makes sense to someone who can’t see the images.

There are a lot of misconceptions of what we mean when we talk about empathy.

| Misconception | Clarification |
| --------- | ----------- |
| I have to use slang and other casual language. | No one is telling you to write phrases like, “Dude, the server is down! That’s a wicked bummer.”  The same rules for everyday language apply here. Choose words that sound natural for your content and your audience. If you aren’t sure how a paragraph sounds, read it out loud or ask someone else to read it for you. |
| Empathy makes a joke out of a serious problem | When done well, empathy lets our readers know that we take their problems seriously. The customer’s perspective is an important part of the solution; when we acknowledge what they are going through, that helps them understand that we are trying to find a solution that works for them. |
| Empathy will undermine our corporate image | Sometimes, in the past, we’ve written articles as if we were lawyers trying to protect our company from blame. There is a time and a place for legal disclaimers– and it is in an official legal disclaimer written by a lawyer, not in a help article. Truthfully, some customers perceive us as being arrogant, condescending, and completely uninterested in how customers feel. If that is how we are being seen, perhaps we should undermine our image. Empathy presents us as real people helping real people. |
| IT Pro and Dev will hate this |  |

### Some things to ask yourself about empathy

- Does the article read like we are their partner?
- Does the article address the customer’s point of view and what matters to them?
- If the situation is genuinely frustrating, does the article acknowledge it?

## A few more questions to ask yourself
- Do I really need this bit of text?
- What happens before this, and what happens after?
- What's the users intent at this moment?
- What must they do now, if anything?
- What do they need to know?
- Have I put the key information, action, or issue first?
- Can I rewrite this in a completely different way that would be more direct?
- What can I cut?
- Is there any redundancy or repetition (in the context of the entire screen and flow)?
- Is there any unnecessary use of brand/feature/product names, jargon, or tech speak?

## Next steps
