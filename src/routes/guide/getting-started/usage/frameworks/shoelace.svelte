<ShoelaceLayout onLoaded={onLoaded}>
    <form id="demoForm" class="form-horizontal" method="POST">
        <div class="row input-field">
            <label class="col-3 control-label">Username</label>
            <div class="col-5">
                <input type="text" name="username" />
            </div>
        </div>
    
        <div class="row input-field">
            <label class="col-3 control-label">Password</label>
            <div class="col-5">
                <input type="password" name="password" />
            </div>
        </div>
    
        <div class="row input-field">
            <div class="col-9 offset-3">
                <button type="submit" class="btn btn-primary">Submit</button>
            </div>
        </div>
    </form>
</ShoelaceLayout>

<script>
import { onDestroy } from 'svelte';

import formValidation from 'formvalidation/dist/es6/core/Core';
import DemoFrame from 'formvalidation/dist/es6/plugins/DemoFrame';
import Icon from 'formvalidation/dist/es6/plugins/Icon';
import Trigger from 'formvalidation/dist/es6/plugins/Trigger';
import Shoelace from 'formvalidation/dist/es6/plugins/Shoelace';
import SubmitButton from 'formvalidation/dist/es6/plugins/SubmitButton';

import sampleCode from './shoelace.programmatic';
import ShoelaceLayout from '../../../../../components/demo/ShoelaceLayout.svelte';

let fv;

const onLoaded = () => {
    fv = formValidation(document.getElementById('demoForm'), {
        fields: {
            username: {
                validators: {
                    notEmpty: {
                        message: 'The username is required'
                    },
                    stringLength: {
                        min: 6,
                        max: 30,
                        message: 'The username must be more than 6 and less than 30 characters long'
                    },
                    regexp: {
                        regexp: /^[a-zA-Z0-9_]+$/,
                        message: 'The username can only consist of alphabetical, number and underscore'
                    }
                }
            },
            password: {
                validators: {
                    notEmpty: {
                        message: 'The password is required'
                    },
                    stringLength: {
                        min: 8,
                        message: 'The password must have at least 8 characters'
                    },
                }
            },
        },
        plugins: {
            trigger: new Trigger(),
            shoelace: new Shoelace(),
            submitButton: new SubmitButton(),
            icon: new Icon({
                valid: 'fa fa-check',
                invalid: 'fa fa-times',
                validating: 'fa fa-refresh',
            }),
            demoFrame: new DemoFrame({
                sender: '/guide/getting-started/usage/frameworks/shoelace',
                sampleCode: sampleCode,
            }),
        },
    });
};

onDestroy(() => {
    fv && fv.destroy();
});
</script>
