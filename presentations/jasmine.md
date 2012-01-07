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


