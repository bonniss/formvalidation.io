<svelte:head>
	<title>FormValidation • Sequence plugin</title>
</svelte:head>

<GuideLayout>
    <h1 class="f3 f2-m f1-l tc">Sequence plugin</h1>
    <h2 class="f4 fw4 tc lh-copy">Stop performing remaining validators if there is a validator that the field does not pass</h2>

    <section class="mv5">
        <Heading>Usage</Heading>
        <p class="lh-copy">By default, when a field is being validated, all validators for a field will be executed. Let's take a look at a simple signing up form that its username field has to pass all of the following validator rules:</p>
<SampleCode lang="javascript" code={`
FormValidation.formValidation(document.getElementById('signupForm'), {
    fields: {
        username: {
            validators: {
                notEmpty: {
                    message: 'The username is required'
                },
                callback: {
                    message: 'This username is not allowed',
                    callback: function(input) {
                        // Do not accept the username starting with "admin"
                        return !input.value.startsWith('admin');
                    }
                },
                stringLength: {
                    min: 6,
                    max: 30,
                    message: 'The username must be more than 6 and less than 30 characters long'
                },
                regexp: {
                    regexp: /^[a-zA-Z0-9_]+$/,
                    message: 'The username can only consist of alphabetical, number and underscore'
                },
                remote: {
                    message: 'The username is already taken',
                    method: 'GET',
                    url: '/path/to/your/back-end/',
                },
            },
        },
    },
    plugins: {
        ...
    },
});
`} />
        <p class="lh-copy">After each key stroke, all validators will perform their jobs. Some of them might be expensive tasks such as checking the validity in the server side via the <a href="/guide/validators/remote" class="blue dim link">remote</a> validator.</p>
        <p class="lh-copy">It is better if the expensive validator is performed at the end when the field passes all other remaining validators. It reduces the number of server side requests (for example, it will not hit the database server to check if an username is taken).
            Also, our users don't have to wait for these validators to run and return the results. It brings a better user experience.</p>
        <p class="lh-copy">The Sequence plugin is handy for this requirement. It will stop performing a given validator if the field does not pass the previous validator.</p>
        <p class="lh-copy">The following piece of code is the starting point to use the Sequence plugin:</p>
<SampleCode lang="html" code={`
<html>
<head>
    <link-tag rel="stylesheet" href="/vendors/formvalidation/dist/css/formValidation.min.css">
</head>
<body>
    <form id="demoForm" method="POST">
        ...
    </form>

<script-tag src="https://cdnjs.cloudflare.com/ajax/libs/es6-shim/0.35.3/es6-shim.min.js"></script-tag>    
<script-tag src="/vendors/formvalidation/dist/js/FormValidation.min.js"></script-tag>

<script-tag>
document.addEventListener('DOMContentLoaded', function(e) {
    FormValidation.formValidation(
        document.getElementById('demoForm'),
        {
            fields: {
                ...
            },
            plugins: {
                sequence: new FormValidation.plugins.Sequence({
                    enabled: true,
                }),
                ...
            },
        }
    );
});
</script-tag>
</body>
</html>
`} />
        <p class="lh-copy">The sample code above assumes that the FormValidation files are placed inside the <code>vendors</code> directory. You might need to change the path depending on where you place them on the server.</p>
    </section>

    <section class="mv5">
        <Heading>Options</Heading>
        <table class="collapse ba br2 b--black-10 pv2 ph3 w-100">
            <tr class="striped--light-gray">
                <th class="pv2 ph3 tl f6 fw6 ttu">Option</th>
                <th class="pv2 ph3 tl f6 fw6 ttu">Type</th>
                <th class="pv2 ph3 tl f6 fw6 ttu">Description</th>
            </tr>
            <tr class="striped--light-gray">
                <td class="pv2 ph3"><code>enabled</code></td>
                <td class="pv2 ph3">Boolean or Object</td>
                <td class="pv2 ph3 lh-copy">It can be
                    <li><code>true</code> (default value)</li>
                    <li><code>false</code></li>
                    <li>or an object indicating a given field will use the behaviour. For example:
<SampleCode lang="javascript" code={`
enabled: {
    username: true,
    // All the validators for password field 
    // will be performed as usual
    password: false,
},
`} />
                    </li>
                </td>
            </tr>
        </table>
    </section>

    <section class="mv5">
        <Heading>Basic example</Heading>
        <p class="lh-copy">In the following form, all validators are performed in sequential order. A validator will not be executed if the field doesn't pass the previous validator.</p>
        <p class="lh-copy">By putting the remote validator at the end, we only send a request to server to check if the username is taken if it passes all other validators.</p>
        <p class="lh-copy">For testing purpose, the demo always answers that the username is already taken no matter what you input.</p>
        <Demo prefix="/guide/plugins/sequence/basic" frameworks={['tachyons']} />
    </section>
    
    <section class="mv5">
        <Heading>Changelog</Heading>
        <ul class="pa0 ma0 ml3 lh-copy">
            <li>v1.1.0: First release. It means that the Sequence plugin requires FormValidation v1.1.0 or newer.</li>
        </ul>
    </section>

    <section class="mv5">
        <div class="flex">
            <PrevButton target="/guide/plugins/semantic">Semantic plugin</PrevButton>
            <NextButton target="/guide/plugins/shoelace">Shoelace plugin</NextButton>
        </div>
    </section>
</GuideLayout>

<script>
import Demo from '../../../../components/Demo.svelte';
import Heading from '../../../../components/Heading.svelte';
import GuideLayout from '../../../../components/GuideLayout.svelte';
import NextButton from '../../../../components/NextButton.svelte';
import PrevButton from '../../../../components/PrevButton.svelte';
import SampleCode from '../../../../components/SampleCode.svelte';
</script>
