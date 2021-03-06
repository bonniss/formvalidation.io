<svelte:head>
	<title>FormValidation • Shoelace plugin</title>
</svelte:head>

<GuideLayout>
    <h1 class="f3 f2-m f1-l tc">Shoelace plugin</h1>
    <h2 class="f4 fw4 tc lh-copy">Integrate with <a href="https://shoelace.style" class="blue dim link">Shoelace</a> library. Support Shoelace v1.0.0-beta24</h2>

    <section class="mv5">
        <Heading>Usage</Heading>
        <p class="lh-copy">The following piece of code is the starting point to validate the form made in Shoelace:</p>
<SampleCode lang="html" code={`
<html>
<head>
    <link-tag rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/shoelace-css/1.0.0-beta24/shoelace.css">
    <link-tag rel="stylesheet" href="/vendors/formvalidation/dist/css/formValidation.min.css">
</head>
<body>
    <form id="demoForm" method="POST">
        ...
    </form>

<script-tag src="https://cdnjs.cloudflare.com/ajax/libs/es6-shim/0.35.3/es6-shim.min.js"></script-tag>    
<script-tag src="/vendors/formvalidation/dist/js/FormValidation.min.js"></script-tag>
<script-tag src="/vendors/formvalidation/dist/js/plugins/Shoelace.min.js"></script-tag>

<script-tag>
document.addEventListener('DOMContentLoaded', function(e) {
    FormValidation.formValidation(
        document.getElementById('demoForm'),
        {
            fields: {
                ...
            },
            plugins: {
                shoelace: new FormValidation.plugins.Shoelace(),
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
            <li><code>Shoelace.min.js</code> is the plugin provided by FormValidation. It is NOT the same as <code>shoelace(.min).js</code> file provided by the Shoelace library.</li>
        </ul>
        <p class="lh-copy">The next sections list out some examples of various forms made with Shoelace.</p>
    </section>

    <section class="mv5">
        <Heading>Horizontal form</Heading>
        <Demo prefix="/guide/plugins/shoelace/horizontal-form" frameworks={['shoelace']} />
    </section>

    <section class="mv5">
        <Heading>Stacked form</Heading>
        <Demo prefix="/guide/plugins/shoelace/stacked-form" frameworks={['shoelace']} />
    </section>

    <section class="mv5">
        <Heading>Multiple fields on the same row</Heading>
        <p class="lh-copy">In order to add the correct class for error message and the field element when it is a valid or invalid, we need to specify the CSS selector of the field container.</p>
        <p class="lh-copy">By default, the Shoelace plugin will look for the <code>.input-field</code> element. In the following example, the <code>firstName</code> and <code>lastName</code>
            fields are placed inside <code>.col-4</code> containers. Meanwhile, the <code>city</code>, <code>state</code> and <code>zipcode</code> fields can be found inside the <code>.col-3</code> containers.
        </p>
        <p class="lh-copy">The <code>rowSelector</code> option will be used to help the plugin determine the field containers as following:</p>
        <div class="mb4">
<SampleCode lang="javascript" code={`
shoelace: new FormValidation.plugins.Shoelace({
    rowSelector: function(field, ele) {
        // field is the field name
        // ele is the field element
        switch (field) {
            case 'firstName':
            case 'lastName':
                return '.col-4';
            
            case 'city':
            case 'state':
            case 'zipcode':
                return '.col-3';
            
            default:
                return '.input-field';
        }
    }
}),
`} />        
        </div>
        <Demo prefix="/guide/plugins/shoelace/multiple-fields" frameworks={['shoelace']} />
    </section>

    <section class="mv5">
        <Heading>Changelog</Heading>
        <ul class="pa0 ma0 ml3 lh-copy">
            <li>v1.0.0: First release</li>
        </ul>
    </section>

    <section class="mv5">
        <div class="flex">
            <PrevButton target="/guide/plugins/sequence">Sequence plugin</PrevButton>
            <NextButton target="/guide/plugins/spectre">Spectre plugin</NextButton>
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
