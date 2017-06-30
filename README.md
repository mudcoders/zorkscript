# ZorkScript

An esoteric scripting language based on text-based game commands.

## Notes

Some notes via the conversation topic in our [Slack channel](https://mudcoders.signup.team/):

### Commands

Some basic command aliases:

- `print "string"` -> `say "string"`
- `new String()` -> `craft String named $var`
- `$var = "value"` -> `put "value" in $var`

### Functions

In ZorkScript, functions are structured like "spells." For example, the following pseudocode:

```
function echo($string) {
  print($string);
}
```

Would look like this in ZorkScript:

```
spell Echo
  component $string
  say "#{$string}"
```

#### Execution

Calling a function is accomplished using the `cast` command, like so:

```
cast Echo with "Hi!"
```

### Classes

Classes follow a similar structure, but are structured like physical objects. For example:

```
class Point {
  private $x;
  private $y;
  
  public function Echo() {
    print("$x, $y");
  }
}
```

Would be structured like this:

```
blueprint Point
  component $x
  component $y
  
  casts Echo with "#{$x}, #{$y}"
```

Function definitions are generally global, however they can be localized within an object similarly to how the Go programming language handles object orientation.

#### Instantiation

Instantiating a class can be accomplished using the `craft` command, like so:

```
craft Point with 1 and 1 named $point
```

This would instantiate the `Point` class defined above, using `1` and `1` for `$x` and `$y` respectively, and assign it to the `$point` variable.

**As a note, an interpreter might tokenize that command like this:**

```
Token(Keyword) "craft"
Token(Identifier) "Point"
Token(ArgList) "with"
    Token(Number) 1
    Token(Seperator) "and"
    Token(Number) 1
Token(Keyword) "named"
Token(VarIdentifier) "$point"
```

#### Instance Methods

Instance methods are called similarly to how global methods are called:

```
cast Echo using $point
```

As you can see, the `Echo` method is called, but within the context of the `$point` class.

### Dependencies

Dependencies can be imported using the `summon` command:

```
summon utilities
```
