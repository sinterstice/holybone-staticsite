---
title: "Tell us about your experiences on the internet!"
params:
    hide_newsletter: true
---

Did you grow up with access to a computer? Did it have a profound effect on the person you are today? Did you make friends, play games, imagine worlds, unlock secret potentials in yourself that no one around you could see? Do you have a feeling that we've forgotten something profound about what the internet *could* be, *should* be?

We think so too. The internet most people experience today is one designed and curated by platforms: a handful of megacorporations, covetous of our attention and interested in nothing but profit have tuned their platforms to be as addicting as possible. We give them our time, our creativity, and our connections to each other. What do we get in return? Crippled attention spans and AI slop. Everyone knows it's a problem, but no one knows what to do about it. Get a flip phone? Disconnect? Give up?

Some of us remember a different vision of the web. One where you could be anyone you wanted, make anything you could imagine; where learning how something was made was as simple as right clicking; where technology *wanted you* to take it apart, tweak it, repurpose it and republish it; all you needed was smarts and creativity. 

That internet is out there still. Between the broken links and dead forums, the deprecated plugins and abandoned code bases, there's a map waiting to be reconstructed, a path to a lost future. We at Holy Bone! Productions are embarking on a journey to explore and document that lost future, so recently and thoughtlessly abandoned, in hopes that the past can show us a way forward: a way out of the culture wars and brain rot, a way to a world that puts the free development of every individual above the profits of platform holders. 

That project can only be one that belongs to all of us. We need your memories, your dreams and failures to piece it together. We'd love to hear anything you'd like to share about what the internet has meant to you, good or bad, lost or thriving.

*Note: All fields are optional. Your answers can be as long or as short as you like. You are safe to close the page; your answers will be cached in your local browser until you submit.*

<style>
.interview-form form {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
}

.interview-form form label {
    margin-bottom: 1rem;
}

.interview-form label span {
    display: inline-block;
    width: 100%;
}

.interview-form label.condensed span {
    width: auto;
}

.interview-form textarea {
width: 100%;
min-height: 4rem;
}
</style>

<div class="interview-form">
    <form id="interview-form">
        <label class="">
            <span>Email</span>
            <input id="email" type="email" class="form-value autosave"/>
        </label>
        <label class=""/>
            <span>Name</span>
            <input id="name" type="text" class="form-value autosave"/>
        </label>
        <label class=""/>
            <span>How old were you when you first got access to the internet?</span>
            <input id="online_age" type="text" class="form-value autosave"/>
        </label>
        <label class=""/>
            <span>What year was that?</span>
            <input id="online_year" type="text" class="form-value autosave"/>
        </label>
        <label class=""/>
            <span>About how many hours a week did you spend in front of a computer?</span>
            <input id="age" type="text" class="form-value autosave"/>
        </label>
        <label class=""/>
            <span>What websites, programs, forums, or chat services did you use most frequently?</span>
            <textarea id="activities" class="form-value autosave"></textarea>
        </label>
        <label class=""/>
            <span>What's something you once loved online that can't be found anymore?</span>
            <textarea id="lost" class="form-value autosave"></textarea>
        </label>
        <label class=""/>
            <span>Did you represent yourself differently online than IRL? Did you feel like a different person online? Which felt more real to you, online or IRL?</span>
            <textarea id="split" class="form-value autosave"></textarea>
        </label>
        <label class=""/>
            <span>Did you ever fall in love with someone you met online? How did you meet them? How did it end?</span>
            <textarea id="love" class="form-value autosave"></textarea>
        </label>
        <label class=""/>
            <span>What part of your life online was kept secret from your friends or family?</span>
            <textarea id="secret" class="form-value autosave"></textarea>
        </label>
        <label class=""/>
            <span>How is the way you engage with the internet now different from when you were younger?</span>
            <textarea id="change" class="form-value autosave"></textarea>
        </label>
        <label class=""/>
            <span>Overall, would you say the impact of the internet on your life has been positive or negative? How so?</span>
            <textarea id="impact" class="form-value autosave"></textarea>
        </label>
        <label class="condensed"/>
            <input type="checkbox" class="form-value" id="followup"/>
            <span>Yes, I want to be contacted for follow up about these answers.</span>
        </label>
        <label class="condensed"/>
            <input type="checkbox" class="form-value" id="followup"/>
            <span>Yes, please notify me about future project updates.</span>
        </label>
        <label class="condensed"/>
            <input type="checkbox" class="form-value" id="usage"/>
            <span>You may quote my answers directly in your project (with special thanks).</span>
        </label>
        <label class="condensed"/>
            <input type="checkbox" class="form-value" id="anonymous"/>
            <span>Please keep my answers anonymous.</span>
        </label>
        <button class="submit" type="submit" id="submit">SUBMIT</button>
        <p id="result"></p>
    </form>
<script>
const form = document.querySelector('#interview-form');
const submit = document.querySelector('#submit');
const result = document.querySelector('#result');
form.addEventListener('submit', (e) => {
    e.preventDefault();
    const body = {};
    Array.from(document.querySelectorAll('.form-value')).forEach((el) => {
        const value = el.value;
        const id = el.id;
        body[id] = value;
    });
    const originalSubmitText = submit.innerText;
    submit.innerText = 'Waiting...';
    submit.disabled = true;
    console.log(body);
    fetch(new Request(`https://api.holybone.zone/api/interview`, {
        method: 'POST',
        mode: 'cors',
        body: JSON.stringify(body)
    })).then((res) => {
        let resultMessage = 'So sorry. Something went wrong.';
        if (res.ok) {
            resultMessage = 'Success! You have signed up';
        }
        window.localStorage.clear();
        result.innerText = resultMessage;
    }, (failure) => {
        submit.innerText = originalSubmitText;
        result.innerText = 'So sorry. Something went wrong.';
    }).finally(() => {
        submit.innerText = originalSubmitText;
        submit.disabled = false;
    });
});
Array.from(document.querySelectorAll('.autosave')).forEach((el) => {
    el.addEventListener('change', (e) => {
        const id = e.target.id;
        const value = e.target.value;
        const currentValue = JSON.parse(window.localStorage.getItem('interviewForm')) || {};
        currentValue[id] = value.trim();
        window.localStorage.setItem('interviewForm', JSON.stringify(currentValue));
    });
});
window.addEventListener('DOMContentLoaded', () => {
    const currentValue = JSON.parse(window.localStorage.getItem('interviewForm')) || {};
    Object.entries(currentValue).forEach(([id, value]) => {
        const el = document.getElementById(id);
        if (!el) {
            console.error(`Could not find element with ID ${id}`);
            return;
        }
        el.value = value;
    });
});
</script>
</div>

