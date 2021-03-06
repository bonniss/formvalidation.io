<svelte:head>
	<title>FormValidation • Materialize plugin</title>
</svelte:head>

<GuideLayout>
    <h1 class="f3 f2-m f1-l tc">Materialize plugin</h1>
    <h2 class="f4 fw4 tc lh-copy">Integrate with <a href="https://materializecss.com" class="blue dim link">Materialize</a> framework. Support Materialize v1.0.0</h2>

    <section class="mv5">
        <Heading>Usage</Heading>
        <p class="lh-copy">The following piece of code is the starting point to validate the form made in Materialize:</p>
<SampleCode lang="html" code={`
<html>
<head>
    <link-tag rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css">
    <link-tag rel="stylesheet" href="/vendors/formvalidation/dist/css/formValidation.min.css">
</head>
<body>
    <form id="demoForm" method="POST">
        ...
    </form>

<script-tag src="https://cdnjs.cloudflare.com/ajax/libs/es6-shim/0.35.3/es6-shim.min.js"></script-tag>
<script-tag src="https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/js/materialize.min.js"></script-tag>
<script-tag src="/vendors/formvalidation/dist/js/FormValidation.min.js"></script-tag>
<script-tag src="/vendors/formvalidation/dist/js/plugins/Materialize.min.js"></script-tag>

<script-tag>
document.addEventListener('DOMContentLoaded', function(e) {
    FormValidation.formValidation(
        document.getElementById('demoForm'),
        {
            fields: {
                ...
            },
            plugins: {
                materialize: new FormValidation.plugins.Materialize(),
                ...
            },
        }
    );
});
</script-tag>
</body>
</html>
`} />
        <p class="lh-copy">There are some important things here:</p>
        <ul class="ma0 pl3 lh-copy">
            <li>The sample code above assumes that the FormValidation files are placed inside the <code>vendors</code> directory. You might need to change the path depending on where you place them on the server.</li>
            <li><code>Materialize.min.js</code> is the plugin provided by FormValidation. It is NOT the same as <code>materialize(.min).js</code> file provided by Materialize framework.</li>
        </ul>
        <p class="lh-copy">The next sections list out some examples of various forms made with Materialize.</p>
    </section>

    <section class="mv5">
        <Heading>Stacked form</Heading>
        <Demo prefix="/guide/plugins/materialize/stacked-form" frameworks={['materialize']} />
    </section>

    <section class="mv5">
        <Heading>Multiple fields on the same row</Heading>
        <p class="lh-copy">In order to add the correct class for error message and the field element when it is a valid or invalid, we need to specify the CSS selector of the field container.</p>
        <p class="lh-copy">By default, the Materialize plugin will look for the <code>.row</code> element. In the following example, the <code>firstName</code> and <code>lastName</code>
            fields are placed inside <code>.s6</code> containers. Meanwhile, the <code>city</code>, <code>state</code> and <code>zipcode</code> fields can be found inside the <code>.s4</code> containers.
        </p>
        <p class="lh-copy">The <code>rowSelector</code> option will be used to help the plugin determine the field containers as following:</p>
        <div class="mb4">
<SampleCode lang="javascript" code={`
materialize: new FormValidation.plugins.Materialize({
    rowSelector: function(field, ele) {
        // field is the field name
        // ele is the field element
        switch (field) {
            case 'firstName':
            case 'lastName':
                return '.s6';
            
            case 'city':
            case 'state':
            case 'zipcode':
                return '.s4';
            
            default:
                return '.row';
        }
    }
}),
`} />        
        </div>
        <Demo prefix="/guide/plugins/materialize/multiple-fields" frameworks={['materialize']} />
    </section>
    
    <section class="mv5">
        <Heading>Changelog</Heading>
        <ul class="pa0 ma0 ml3 lh-copy">
            <li>v1.2.0: First release. It means that the Materialize plugin requires FormValidation v1.2.0 or newer.</li>
        </ul>
    </section>

    <section class="mv5">
        <div class="flex">
            <PrevButton target="/guide/plugins/mandatory-icon">MandatoryIcon plugin</PrevButton>
            <NextButton target="/guide/plugins/message">Message plugin</NextButton>
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
