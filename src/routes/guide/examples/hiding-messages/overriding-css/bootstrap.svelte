<style>
:global(.fv-plugins-bootstrap .form-group.row.selectContainer .fv-plugins-icon) {
    right: -20px;
}
:global(.fv-plugins-message-container) {
    display: none;
}
</style>

<BootstrapLayout onLoaded={onLoaded}>
    <form id="demoForm" method="POST">
        <div class="form-group row">
            <label class="col-sm-3 col-form-label">Bug title</label>
            <div class="col-sm-6">
                <input type="text" class="form-control" name="title" />
            </div>
        </div>
    
        <div class="form-group row">
            <label class="col-sm-3 col-form-label">Description</label>
            <div class="col-sm-6">
                <textarea class="form-control" name="description" rows="8"></textarea>
            </div>
        </div>
    
        <div class="form-group row">
            <label class="col-sm-3 col-form-label">Operating system</label>
            <div class="col-sm-9">
                <div class="form-check form-check-inline">
                    <input type="radio" class="form-check-input" name="os" value="window" />
                    <label class="form-check-label">Window</label>
                </div>
                <div class="form-check form-check-inline">
                    <input type="radio" class="form-check-input" name="os" value="centos" />
                    <label class="form-check-label">Centos</label>
                </div>
                <div class="form-check form-check-inline">
                    <input type="radio" class="form-check-input" name="os" value="fedora" />
                    <label class="form-check-label">Fedora</label>
                </div>
                <div class="form-check form-check-inline">
                    <input type="radio" class="form-check-input" name="os" value="ubuntu" />
                    <label class="form-check-label">Ubuntu</label>
                </div>
                <div class="form-check form-check-inline">
                    <input type="radio" class="form-check-input" name="os" value="macos" />
                    <label class="form-check-label">macOS</label>
                </div>
            </div>
        </div>
    
        <div class="form-group row">
            <label class="col-sm-3 col-form-label">Browser(s)</label>
            <div class="col-sm-9">
                <div class="form-check form-check-inline">
                    <input type="checkbox" class="form-check-input" name="browser[]" value="ie" />
                    <label class="form-check-label">IE</label>
                </div>
                <div class="form-check form-check-inline">
                    <input type="checkbox" class="form-check-input" name="browser[]" value="chrome" />
                    <label class="form-check-label">Chrome</label>
                </div>
                <div class="form-check form-check-inline">
                    <input type="checkbox" class="form-check-input" name="browser[]" value="firefox" />
                    <label class="form-check-label">Firefox</label>
                </div>
                <div class="form-check form-check-inline">
                    <input type="checkbox" class="form-check-input" name="browser[]" value="safari" />
                    <label class="form-check-label">Safari</label>
                </div>
                <div class="form-check form-check-inline">
                    <input type="checkbox" class="form-check-input" name="browser[]" value="opera" />
                    <label class="form-check-label">Opera</label>
                </div>
            </div>
        </div>
    
        <div class="form-group row selectContainer">
            <label class="col-sm-3 col-form-label">Priority</label>
            <div class="col-sm-4">
                <select class="form-control" name="priority">
                    <option value="">Choose the priority</option>
                    <option value="low">Low</option>
                    <option value="medium">Medium</option>
                    <option value="high">High</option>
                </select>
            </div>
        </div>
    
        <div class="form-group row">
            <div class="col-sm-9 offset-sm-3">
                <button type="submit" class="btn btn-primary">Report issue</button>
            </div>
        </div>
    </form>
</BootstrapLayout>

<script>
import { onDestroy } from 'svelte';

import formValidation from 'formvalidation/dist/es6/core/Core';
import DemoFrame from 'formvalidation/dist/es6/plugins/DemoFrame';
import Icon from 'formvalidation/dist/es6/plugins/Icon';
import Trigger from 'formvalidation/dist/es6/plugins/Trigger';
import Bootstrap from 'formvalidation/dist/es6/plugins/Bootstrap';
import SubmitButton from 'formvalidation/dist/es6/plugins/SubmitButton';

import sampleCode from './bootstrap.programmatic';
import BootstrapLayout from '../../../../../components/demo/BootstrapLayout.svelte';

let fv;

const onLoaded = () => {
    fv = formValidation(document.getElementById('demoForm'), {
        fields: {
            title: {
                validators: {
                    notEmpty: {
                        message: 'The title is required'
                    }
                }
            },
            description: {
                validators: {
                    notEmpty: {
                        message: 'The abstract is required'
                    }
                }
            },
            os: {
                validators: {
                    notEmpty: {
                        message: 'The operating system is required'
                    }
                }
            },
            'browser[]': {
                validators: {
                    notEmpty: {
                        message: 'Choose at least one browser'
                    }
                }
            },
            priority: {
                validators: {
                    notEmpty: {
                        message: 'The priority is required'
                    }
                }
            },
        },
        plugins: {
            trigger: new Trigger(),
            bootstrap: new Bootstrap(),
            submitButton: new SubmitButton(),
            icon: new Icon({
                valid: 'fa fa-check',
                invalid: 'fa fa-times',
                validating: 'fa fa-refresh',
            }),
            demoFrame: new DemoFrame({
                sender: '/guide/examples/hiding-messages/overriding-css/bootstrap',
                sampleCode: sampleCode,
            }),
        },
    });
};

onDestroy(() => {
    fv && fv.destroy();
});
</script>
