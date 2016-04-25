# TODO

Current implementation is very inefficient and has only shallow constness
reports. Besides it only reports the constness problems instead of fixing it.

As an epic, I would create this as a standalone tool (on top of tooling
library) and implement a constness rewrite tool.

- Split the codebase into tool/plugin. The tool would take a compilation
  database, do the constness alalyzis and fix candidates. While the plugin
  could be only for testing purposes.

- Do deeper analyzis on constness. Currently only the value analyzis is done.
  If a pointer to a data structure does not mutate the data structure,
  it could be defined as a pointer to a const object. (Currently it is not
  implemented.)

- For better findings, maybe, a callgraph generation would be usefull.
  (And do analyzis in topological order.)

- General idea to fix the inefficient implementation is to first generate an
  event list from every files. The events could be: variable declared,
  variable mutated, variable accessed, variable out of scope, function called,
  class declared, etc... And after the event stream generated, a post
  processing could come up with constness candidates. Which might be passed
  to a rewrite functionality. This way we travers the AST only once.
