# JavaScript Unit Testing with Jasmine

---

# What is Jasmine?

* BDD framework for testing JavaScript
* Brought to you by the good folks at Pivotal Labs (Privotal Tracker) 
* JS framework independent
* Can be run from a static web page, CI environment or server-side environment (Node.js)
* [http://pivotal.github.com/jasmine/](http://pivotal.github.com/jasmine/)

---

# Example

	!javascript
	describe("sample test", function(){
		it("tests addition", function(){
			expect(2 + 2).toEqual(4);
		});
	});

---

# Setup: Static HTML

* Download Jasmine standalone
* Create a Spec runner html file ([template](https://github.com/pivotal/jasmine/blob/master/lib/jasmine-core/example/SpecRunner.html))
* Update with your source and test files
* Fire it up in a browser
* [Demo](http://jsfiddle.net/diazruy/zqcVB/)

---

# Setup: Rails (jasmine-gem)

* Add jasmine to your Gemfile

		!ruby
		gem 'jasmine', :group => [:development, :test]

* Bootstrap jasmine

		!sh
		$ bundle
		$ rails generate jasmine:install

* Run the specs

		!sh
		$ rake jasmine # or rake jasmine:ci
		$ open localhost:8888

* Configure Jasmine
	* `spec/javascripts/support/jasmine.yml`
	* `spec/javascripts/support/jasmine_config.rb`

---

# jasmine.yml

	!yaml
	# Source directory path. Will use root if left blank
	src_dir:
		- "."
	# Array of filepaths relative to src_dir. Included before jasmine specs
	src_files:
		- "public/javascripts/jquery.js"
		- "public/javascripts/**/*.js"
		# Might want to include files manually to prevent dependency issues
	spec_dir:
		- "spec/javascripts"
	# Array of filepaths relative to spec_dir
	spec_files:
		- "**/*[sS]pec.js"
	# Included before jasmine specs
	helpers:
		- "helpers/**/*.js"

---

# Specs

	!javascript
	it("should do something", function(){
		// Test goes here
	});

---

# Suites

	!javascript
	describe("a group of examples", function(){
		var foo
		// it("should do...")
		// it("should do...")

		describe("a nested scope", function(){
			// it("should do...")
			// it("should do...")
		});
	});

---

# Before/After callbacks

* `beforeEach`
* `afterEach`

` `

	!javascript
	beforeEach(function(){
		// This will run before every spec in all suites 
	});

	describe("a suite", function() {
		var foo;

		beforeEach(function(){
			foo = 1;
		});

		it('should use the value from the beforeEach block', function(){
			expect(foo).toEqual(1);
		});
	});
---

# Expectations and Matchers

* `toEqual` - equivalence
* `toBe` - identity
* `toMatch` - regex
* `toBeDefined`/`toBeUndefined`
* `toBeNull`
* `toBeTruthy`/`toBeFalsy`
* `toContain` - arrays or strings
* `toBeLessThan`/`toBeGreaterThan`
* `expect(function(){ fin(); }).toThrow(e)`
* and [more](http://pivotal.github.com/jasmine/jsdoc/symbols/jasmine.Matchers.html)

Invert criteria with `'.not'`

	!javascript
	expect(x).not.toEqual(y)

---

# jasmine-jquery

* Place it in spec/javascript/support
* Adds jQuery matchers
	* `toBeChecked`, `toBeEmpty`, `toBeHidden`, `toBeSelected`, `toContain`, `toHaveAttribute`, `toHaveHtml`, `toHaveId`, `toBeDisabled`, `toHandle`, and more
* Adds Fixture support
	* `loadFixtures(htmlURL)`
* Adds event spies
	* `spyOnEvent`
	* `toHaveBeenTriggeredOn`

---

# Disabling Tests and Suites

* `xit` - disable a spec
* `xdescribe` - disable a suite

`  `
 
	!javascript
	describe("this suite will execute", function(){
		it("should execute this test", function(){ });

		xit("should not execute this test", function(){ });

		xdescribe("this suite will not execute", function(){
			it("should not execute this test inside the skipped suite", function(){});
		});
	});

---

# Spies

Spying, mocking and faking behaviours.

	!javascript
	describe("a spy", function(){
		it("should spy on an intance method", function(){
			var foo = {
				bar: function(arg){ return arg.toLowerCase(); }
			};

			spyOn(foo, 'bar').andReturn('stubbed');
			// also available: andCallThrough, andCallFake, andThrow
			
			foo.bar('value');

			expect(foo.bar).toHaveBeenCalledWith('value');
		});
	});

---

# Asynchronous specs

* `runs(fn)` - run as if called directly, serially, shared `this`
* `waits(timeout)` - provide a timeout before next block is run
* `waitsFor` - pause until some other work is completed

` `

	!javascript
	describe('a long running process', function(){
		it('should do something asynchronouse', function(){
			var foo = new Foo();
			foo.someAsynchronousStuff();

			waitsFor(function(){
				return foo.isReady();
			}, "Foo did not complete", 10000);

			runs(function(){
				expect(foo.value).toEqual('AJAX retrieved value');
			});
		});
	});

---

# Custom Matchers

Call `this.addMatchers()` from within `before` or `it` block

	!javascript
	beforeEach(function(){
		this.addMatchers({
			toBeLessThan: function(expected){
				return this.actual < expected;
			}
		});
	});

---

# Links

* API - [http://pivotal.github.com/jasmine/jsdoc/index.html](http://pivotal.github.com/jasmine/jsdoc/index.html)
* Jasmine Wiki - [https://github.com/pivotal/jasmine/wiki](https://github.com/pivotal/jasmine/wiki)
* Try Jasmine on your Browser - [http://tryjasmine.com/](http://tryjasmine.com/)
* jasmine-jquery - [https://github.com/velesin/jasmine-jquery](https://github.com/velesin/jasmine-jquery)
* Jasmine Headless Webkit - [http://johnbintz.github.com/jasmine-headless-webkit/](http://johnbintz.github.com/jasmine-headless-webkit/)
* Sinon.js - [http://sinonjs.org/](http://sinonjs.org/)
* Railscasts - [http://railscasts.com/episodes/261-testing-javascript-with-jasmine](http://railscasts.com/episodes/261-testing-javascript-with-jasmine)
* HTML5 slides markdown - [ https://github.com/adamzap/landslide ](https://github.com/adamzap/landslide)

---

# Questions

