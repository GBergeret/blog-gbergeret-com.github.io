# Should we automate everything with HCL?

It’s been decades since we've been trying to automate every repeating tasks with imperative
languages (i.e. python, bash). This has enabled us to save time and reduce
errors rate. However it isn’t ideal as it requires to think about every single
scenarios: creation, deletion or updates.
That’s where [DSL](https://en.wikipedia.org/wiki/Domain-specific_language)
languages (i.e. HCL) are awesome! You simply need to describe what you want and the language takes care of every
cases (i.e. what to do if does/does not exist). Therefore you can avoid some hassles and focus on the
smart ideas, critical for your business.

## Write what matters
Do what matter, be an author of smart ideas, not an executioner. As briefly
explained previously, DSL allow you to focus on what’s important and to only write
the final goal. As an example, if you want two instances, you only want to say: "I
want two instances". You shouldn't need to explain in details what to do to create those.
If only one exists, it should create an additional one. If two have already
been created but with other properties than the expected ones, they should be replaced. DSL handles these scenarios seamlessly.

For instance the following piece of code is enough to create, delete or update
an AWS instance without writing tens of lines of code.
```hcl
resource "aws_instance" "i" {
  instance_type = "t3.medium"
  ami           = "ami-abcdefghi"
}
```

This is also partially thanks to the fact that DSL brings idempotence and reduces
the number of edge cases.

## Backed Up and Reviewable
As everything is now coded, you know at any time that your code base reflects your
existing infrastructure. Typically, Git becomes a good place to store the state of
your infrastructure (in some way, a reliable backup).

Furthermore, with Infrastructure as Code instead of manual creation, you can now
introduce a pull requests review process. This allows several people
to validate what’s meant to be done before it’s executed. DSL languages will
dramatically reduce the quantity of code written and so make reviews much more
efficient and simple.

## Reduce knowledge gap
As we now use pull request reviews, more people get a chance to check and be aware of
what's going on. That way you reduce knowledge gap across your team.

## Increase reproducibility
By writing everything you do, you make it reproducible as nothing is left
out of the code base. This is very useful if all the infrastructure needs to be
recreated for some reasons such as a compromised infrastructure or a new environment
required. Also, if this is now reproducible we can start using testing frameworks
in order to test a chunk of infrastructure before deploying it or updating it.
That way you also increase you level of confidence in your infrastructure as
code.

## No need of documentation
Finally, with DSL, you write everything you do in a self-explanatory fashion. You can save
time and energy since you don’t need to document, as it would be the case with manually managed infrastructure.
This is extremely valuable as this not only saves you energy from writing
documentation but also allows new team members to focus on essential things, rather than having to read
documentations which may actually be outdated!

To re-use the piece of code from before, we can see that it is
self-explanatory and so documentation become redundant (or at least very minimal)
```hcl
resource "aws_instance" "consul" {
  instance_type = "t3.medium"
  ami           = "ami-abcdefghi"  # Ubuntu 20.04
}
```

## Even further...
In some case DSL languages can be very verbose as they want to offer an unlimited
quantity of customization. That's when you may want to bring some abstraction
layers in order to simplify the language and define a set of strict values. You
can always implement functions or modules which define some business logic.

_Don’t go too far, don’t use imperative language to generate DSL xD_
