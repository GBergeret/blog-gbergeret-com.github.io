# Should we automate everything with HCL?

It’s been decades we are trying to automate every repeating tasks with imperative
language (i.e. python, bash). This way we've been able to save time and reduce
error rate. However this isn’t great as it requires to think about every single
case: creation, deletion or updates.
That’s where [DSL](https://en.wikipedia.org/wiki/Domain-specific_language)
languages (i.e. HCL) are awesome! You simply need to describe what you want (the
smart idea, critical for your business) and the language takes care of every
cases (i.e. what to do if it exists? what to do if it doesn’t exist).

## Write what matters
Do what matter, be an author of smart ideas, not an executioner. As briefly
explained previously, DSL allow you to focus on what’s important and only write
the smart idea. For instance if you want two instances, you only want to say: I
want two instances. You shouldn't need to explain what to do to have two
instances if none are present, but also if only one exists or if two have already
been created but with other properties than the expected one.

For instance to following peace of code is enough to create, delete or update
an AWS instance without writing tens of lines of code.
```hcl
resource "aws_instance" "i" {
  instance_type = "t3.medium"
  ami           = "ami-abcdefghi"
}
```

This is also partially thanks to the fact that DSL brings idempotence and reduce
the number of edge case.

## Backed Up and Reviewable
As everything is now coded you know at any time that your code reflect your
existing infrastructure and so this makes Git a good place to store the state of
your infrastructure (in some way a BackUp).

Not only, with Infrastructure as Code instead of manual creation you can now
introduce a pull request review process and so make sure several people
can check what’s meant to be done before it’s executed. DSL language will
dramatically reduce the quantity of code written and so make review much more
efficient and simple.

## Reduce knowledge gap
As we now use pull request review, more people get a chance to check and know
what's going on. That way you reduce knowledge gap across your team.

## Increase reproducibility
By writing everything you do, you make everything reproducible as nothing is left
out of the code base. This is very helpful if the all infrastructure needs to be
recreated for some reason (i.e. compromised infrastructure, new environment
required). Also if this is now reproducible we can start using testing framework
in order to test a chunk of infrastructure before deploying it or updating it.
That way you also increase you level of confidence in your infrastructure as
code.

## No need of documentation
Finally, if you write everything you do in a self explanatory way you can save
time and energy as you don’t need to document what you would have done manually.
This is extremely valuable as this not only save you energy from writing
documentation but also save the energy of you new team members energy to read
documentations which may be actually outdated!

To reuse the peace of code from before, we can see that it can be
self-explanatory and so documentation become redundant (or at least very minimum)
```hcl
resource "aws_instance" "consul" {
  instance_type = "t3.medium"
  ami           = "ami-abcdefghi"  # Ubuntu 20.04
}
```

## Even further...
In some case DSL languages can be very verbose as they want to offer an unlimited
quantity of customization. That's when you may want to bring some abastraction
layer in order to simplify the language and define a set of strict values. You
can always implement functions or modules which define some business logic.

_Don’t go too far, don’t use imperative language to generate DSL xD_
