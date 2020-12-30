
<h1>Contininuous Testing Snippets</h1>

<ul>
<li><a href="#mocha"></a>Mocha</li>
<li><a href="#.nightwatch"></a>Nightwatch</li>
<li><a href=".jenkins"></a>Jenkins</li>
</ul>

<h2>Unit Testing</h2>
<h3 class="mocha">Mocha Tests</h3>
<h4>Setup</h4>
<div>
    <h5>Comand Line:</h5>
    Install Mocha by running:
    <pre>
        <code>
            npm install --save-dev mocha
        </code>
    </pre>
    Install Chai by running:
    <pre>
        <code>
            npm i --save-dev chai 
        </code>
    </pre>
    <h5>Test Example Test File:</h5> 
    <pre>
        <code>
            var assert = require('assert');
                describe('Array', function() {
                describe('#indexOf()', function() {
                    it('should return -1 when the value is not present', function() {
                    assert.equal([1, 2, 3].indexOf(4), -1);
                    });
                });
            });
        </code>
    </pre>  
    <h5>Test Script</h5>
    Set up a test script in package.json:
    <pre>
        <code>
            "scripts": {
                "test": "mocha"
            }  
        </code>
    </pre>
    <h5>Run Test</h5>
    <pre>
        <code>
            npm test
        </code>
    </pre>
</div>

<h4>Mocha Tools/Snippest</h4>
<div>
    <h5>describe()</h5>
    describe() - is simply a way to group tests in Mocha. Describe() takes two arguments,
    the first is the name of the test group, and the second is a callback function.    
</div>
Snippet:
<pre>
    <code>
        describe('string name', function(){
            // can nest more describe()'s here, or tests go here
        });
    </code>
</pre>
<div>
    <h5>it()</h5>
    it() is used for an individual test case. it() should be written as if you were saying it out loud: 
    “It should equal zero”, “It should log the user in”, etc. it() takes two arguments, a string explaining 
    what the test should do, and a callback function which contains our actual test: 
</div>
Snippet:
<pre>
    <code>
        it('should...', function(){
            // Test case goes here
        });
    </code>
</pre>
<div>
    <h5>Assert</h5>
    Assert - There are a number of different assertion tests included with assert. 
    Chai provides the following assertion styles:
</div>
<a href="https://www.chaijs.com/api/assert/">Assert Style:</a>
<pre>
<code>
var assert = require('chai').assert;
var numbers = [1, 2, 3, 4, 5];

assert.isArray(numbers, 'is array of numbers');
assert.include(numbers, 2, 'array contains 2');
assert.lengthOf(numbers, 5, 'array contains 5 numbers');
</code>
</pre>
Expect style:   
<pre>
<code>
var expect = require('chai').expect;
var numbers = [1, 2, 3, 4, 5];

expect(numbers).to.be.an('array').that.includes(2);
expect(numbers).to.have.lengthOf(5);
</code>
</pre>
Should style:
<pre>
<code>
var should = require('chai').should();
var numbers = [1, 2, 3, 4, 5];

numbers.should.be.an('array').that.includes(2);
numbers.should.have.lengthOf(5);
</code>
</pre>
<h5>Example</h5>
<pre>
<code>
// Require the built in 'assertion' library
var assert = require('assert');
// Create a group of tests about Arrays
describe('Array', function() {
    // Within our Array group, Create a group of tests for indexOf
    describe('#indexOf()', function() {
        // A string explanation of what we're testing
        it('should return -1 when the value is not present', function(){
            // Our actual test: -1 should equal indexOf(...)
            assert.equal(-1, [1,2,3].indexOf(4));
        });
    });
});
</code>
</pre>

<h2>End to End Testing</h2>
<h3 class="nightwatch">Nightwatch Tests</h3>
<h4>Setup</h4>
<div>
    To run Nightwatch locally we will need a standalone Selenium server locally, as well as a webdriver, so we can use Chrome/Firefox to test our applications locally.
</div>
<h6>Prequisite:</h6>
<a href="https://www.oracle.com/java/technologies/javase-downloads.html">JDK</a> Needs to be installed
<h5>Comand Line:</h5>
Add nightwatch to you project by running:
<pre>
<code>
npm install nightwatch geckodriver chromedriver --save-dev
</code>
</pre>
<p>
    Test successfull installation by running:
</p> 
<code>
npx nightwatch node_modules/nightwatch/examples/tests/ecosia.js
</code>
<h6>Running Tests</h6>
Global
<pre>
<code>
    nightwatch [source] [options]
</code>
</pre>
Project specific
<pre>
<code>
    npx nightwatch [source] [options]
</code>
</pre>
Example - single test:
<pre>
<code>
    nightwatch tests/one/firstTest.js
</code>
</pre>
Example - 2 individual tests:
<pre>
<code>
    nightwatch tests/one/firstTest.js tests/secondTest.js
</code>
</pre>
Example - 1 individual test and 1 folder:
<pre>
<code>
    nightwatch tests/one/test.js tests/utils
</code>
</pre>
<p>
    Test Example:
</p> 
<pre>
<code>
module.exports = {
    'Demo test Google' : function (client) {
        client
        .url('http://www.google.com')
        .waitForElementVisible('body', 1000)
        .assert.title('Google')
        .assert.visible('input[type=text]')
        .setValue('input[type=text]', 'rembrandt van rijn')
        .waitForElementVisible('button[name=btnG]', 1000)
        .click('button[name=btnG]')
        .pause(1000)
        .assert.containsText('ol#rso li:first-child',
            'Rembrandt - Wikipedia')
        .end()
    }
}
</code>
</pre>
<h4>Tools:</h4>
<div>
<h5><a href="https://nightwatchjs.org/api/">Assertions</a></h5>
<div>
    .assert - when an assertion fails, the test ends, skipping all other assertions.
</div>
<div>
    .verify - when an assertion fails, the test logs the failure and continues with other assertions.
</div>
</div>
<br>
assert[.not].attributeContains()
<pre>
<code>
    this.demoTest = function (browser) {
        browser.assert.attributeContains('#someElement', 'href', 'google.com');
    };  
</code>
</pre>
assert[.not].attributeEquals()
<pre>
<code>
    this.demoTest = function (browser) {
        browser.assert.attributeEquals("body", "data-attr", "some value");
    };
</code>
</pre>
assert[.not].containsText()
<pre>
<code>
    this.demoTest = function (browser) {
        browser.assert.containsText("#main", "The Night Watch");
    };
</code>
</pre>
assert[.not].cssClassPresent()
<pre>
<code>
    this.demoTest = function (browser) {
        browser.assert.cssClassPresent("#main", "container");
        browser.assert.cssClassPresent('#main', ['visible', 'container']);
        browser.assert.cssClassPresent('#main', 'visible container');
    };
</code>
</pre>
assert[.not].cssProperty()
<pre>
<code>
    this.demoTest = function (browser) {
        browser.assert.cssProperty("#main", "display", "block");
    };
</code>
</pre>
assert[.not].domPropertyContains()
<pre>
<code>
    this.demoTest = function (browser) {
        browser.assert.domPropertyContains('#main', 'classList', 'visible');
      
        // in case the resulting property is an array, several elements could be specified
        browser.assert.domPropertyEquals('#main', 'classList', ['class-one', 'class-two']);
        browser.assert.domPropertyEquals('#main', 'classList', 'class-one,class-two');
    };
</code>
</pre>
assert[.not].domPropertyEquals()
<pre>
<code>
    this.demoTest = function (browser) {
        browser.assert.domPropertyEquals('#main', 'className', 'visible');
      
        // deep equal will be performed
        browser.assert.domPropertyEquals('#main', 'classList', ['class-one', 'class-two']);
      
        // split on ',' and deep equal will be performed
        browser.assert.domPropertyEquals('#main', 'classList', 'class-one,class-two']);
    };
</code>
</pre>
assert[.not].elementPresent()
<pre>
<code>
    this.demoTest = function (browser) {
        browser.assert.elementPresent("#main");
    };
</code>
</pre>
assert[.not].title()
<pre>
<code>
    this.demoTest = function (browser) {
        browser.assert.title("Nightwatch.js");
    };      
</code>
</pre>
assert[.not].urlContains()
<pre>
<code>
    this.demoTest = function (browser) {
        browser.assert.urlContains('nightwatchjs.org');
    };
</code>
</pre>
assert[.not].urlEquals()
<pre>
<code>
    this.demoTest = function (browser) {
        browser.assert.urlEquals('https://www.google.com');
    };
</code>
</pre>
assert[.not].value()
<pre>
<code>
    this.demoTest = function (browser) {
        browser.assert.value("form.login input[type=text]", "username");
    };
</code>
</pre>
assert[.not].valueContains()
<pre>
<code>
    this.demoTest = function (browser) {
        browser.assert.valueContains("form.login input[type=text]", "username");
    };
</code>
</pre>
assert[.not].visible()
<pre>
<code>
    this.demoTest = function (browser) {
        browser.assert.visible('.should_be_visible');
        browser.assert.visible({selector: '.should_be_visible'});
        browser.assert.visible({selector: '.should_be_visible', supressNotFoundErrors: true});
    };
</code>
</pre>
<h5><a href="https://nightwatchjs.org/api/expect/">Expect</a></h5>
Language Chains
<p>The following are provided as chainable getters to improve the readability of your assertions. They do not provide testing capabilities and the order is not important.</p>
<ul>
<li>to</li>
<li>be</li>
<li>been</li>
<li>is</li>
<li>that</li>
<li>which</li>
<li>and</li>
<li>has</li>
<li>have</li>
<li>with</li>
<li>at</li>
<li>does</li>
<li>of</li>
</ul>
.equal(value)/.contain(value)/.match(regex)
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.element('#main').text.to.equal('The Night Watch');
    
    browser.expect.element('#main').text.to.contain('The Night Watch');
    
    browser.expect.element('#main').to.have.css('display').which.equals('block');
};
</code>
</pre>
.startWith(value)/.endWith(value)
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.element('#main').text.to.endWith('Watch');
    
    browser.expect.element('#main').text.to.startWith('The');
};
</code>
</pre>
.not
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.element('#main').text.to.not.equal('The Night Watch');
    
    browser.expect.element('#main').text.to.not.contain('The Night Watch');
    
    browser.expect.element('#main').to.have.css('display').which.does.not.equal('block');
};
</code>
</pre>
.before(ms)/.after(ms)
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.element('#main').text.to.contain('The Night Watch').before(1000);
    
    browser.expect.element('#main').text.to.not.contain('The Night Watch').after(500);
};      
</code>
</pre>
expect.cookie()
<pre>
<code>
browser.expect.cookie('cookie-name', ['cookie-domain'])
</code>
</pre>
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.cookie('cookie-name').to.contain('cookie-value');
    browser.expect.cookie('cookie-name').to.match(/regex/);
    browser.expect.cookie('loginCookie', 'example.org').to.contain('cookie-value');
};
</code>
</pre>
expect.element()
<pre>
<code>
    browser.element('#selector')
</code>
</pre>
.a(type)Suggest edits
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.element('#q').to.be.an('input');
    browser.expect.element('#q').to.be.an('input', 'Testing if #q is an input');
    browser.expect.element('#w').to.be.a('span');
}
</code>
</pre>
.active
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.element('#main').to.be.active;
    browser.expect.element('#main').to.not.be.active;
    browser.expect.element('#main').to.be.active.before(100);
};
</code>
</pre>
.attribute(name)
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.element('body').to.have.attribute('data-attr');
    browser.expect.element('body').to.not.have.attribute('data-attr');
    browser.expect.element('body').to.not.have.attribute('data-attr', 'Testing if body does not have data-attr');
    browser.expect.element('body').to.have.attribute('data-attr').before(100);
    browser.expect.element('body').to.have.attribute('data-attr')
        .equals('some attribute');
    browser.expect.element('body').to.have.attribute('data-attr')
        .not.equals('other attribute');
    browser.expect.element('body').to.have.attribute('data-attr')
        .which.contains('something');
    browser.expect.element('body').to.have.attribute('data-attr')
        .which.matches(/^something\ else/);
};
</code>
</pre>
.css(property)
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.element('#main').to.have.css('display');
    browser.expect.element('#main').to.have.css('display', 'Testing for display');
    browser.expect.element('#main').to.not.have.css('display');
    browser.expect.element('#main').to.have.css('display').before(100);
    browser.expect.element('#main').to.have.css('display').which.equals('block');
    browser.expect.element('#main').to.have.css('display').which.contains('some value');
    browser.expect.element('#main').to.have.css('display').which.matches(/some\ value/);
};
</code>
</pre>
.enabled
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.element('#weblogin').to.be.enabled;
    browser.expect.element('#main').to.not.be.enabled;
    browser.expect.element('#main').to.be.enabled.before(100);
};
</code>
</pre>
.present
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.element('#main').to.be.present;
    browser.expect.element('#main').to.not.be.present;
    browser.expect.element('#main').to.be.present.before(100);
};
</code>
</pre>
.property(name)
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.element('body').to.have.property('className').equals('test-class');
    browser.expect.element('body').to.have.property('className').matches(/^something\ else/);
    browser.expect.element('body').to.not.have.property('classList').equals('test-class');
    browser.expect.element('body').to.have.property('classList').deep.equal(['class-one', 'class-two']);
    browser.expect.element('body').to.have.property('classList').contain('class-two');
};
</code>
</pre>
.selected
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.element('#main').to.be.selected;
    browser.expect.element('#main').to.not.be.selected;
    browser.expect.element('#main').to.be.selected.before(100);
};
</code>
</pre>
.text
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.element('#main').text.to.equal('The Night Watch');
    browser.expect.element('#main').text.to.not.equal('The Night Watch');
    browser.expect.element('#main').text.to.equal('The Night Watch').before(100);
    browser.expect.element('#main').text.to.contain('The Night Watch');
    browser.expect.element('#main').text.to.match(/The\ Night\ Watch/);
};
</code>
</pre>
.value
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.element('#q').to.have.value.that.equals('search');
    browser.expect.element('#q').to.have.value.not.equals('search');
    browser.expect.element('#q').to.have.value.which.contains('search');
    browser.expect.element('#q').to.have.value.which.matches(/search/);
};
</code>
</pre>
.visible
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.element('#main').to.be.visible;
    browser.expect.element('#main').to.not.be.visible;
    browser.expect.element('#main').to.be.visible.before(100);
};
</code>
</pre>
expect.elements()
<pre>
<code>
    browser.elements('#selector')
</code>
</pre>
.elements().count
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.elements('div').count.to.equal(10);
    browser.expect.elements('p').count.to.not.equal(1);
}
</code>
</pre>

<pre>
.expect.title()
<code>
this.demoTest = function (browser) {
    browser.expect.title().to.contain('value');
    browser.expect.title().to.match(/value/);
};
</code>
</pre>
.expect.url()
<pre>
<code>
this.demoTest = function (browser) {
    browser.expect.url().to.contain('https://');
    browser.expect.url().to.endWith('.org');
};
</code>
</pre>
<h5><a href="https://nightwatchjs.org/api/commands/">API Commands</a></h5>

<h2>Continuous Testing</h2>
<h3><a href="https://www.tutorialspoint.com/jenkins/jenkins_automated_testing"></a>Jenkins</h3>
