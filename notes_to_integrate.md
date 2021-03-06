Use @ for module constants

align guards with the function definition
if guard is longer than one line separate, start each new line aligned with the first clause starting with the predicate

```
def create(VillageState[village_id: id, owner_char_id: owner_id] = village_state)
when id != :undefined 
     and :erlang.is_binary(id) do
```

when any arguments are longer than a line, split each argument into a separate line

indent |> to 2 spaces past the start of base argument

```
initial_value
  |> process_value
  |> process_value_again
    
```

@spec all methods except for behaviour callbacks

@doc for all public apis of a module

## Records

Prefer `RecordName.record_value(new_value, record)` over `record.record_value(new_value)` for ease of refactoring

Prefer `RecordName.new` to `RecordName[]`


## Control Flow

Prefer pattern matching over control flow (case, if, etc..) in order to encourage functional design patterns

```
# bad
def print(value)
  case value do
  0 -> IO.puts "value is 0"
  1 -> IO.puts "value is 1"
  default -> IO.puts "value is not 0 or 1"
end

# good
def print(0)
  IO.puts "value is 0"
end
def print(1)
  IO.puts "value is 1"
end
def print(other)
  IO.puts "value is not 0 or 1"
end


```

## Return values
In cases of return success/error values, have the module return either the atom `:ok` or the tuple `{:error, reason}` where reason is some atom the desribes the error.

```
# good
def validate(true), do: :ok
def validate(false), do: {:error, :not_true}

```

## Module Naming
Module naming should be separated by `.` when nested inside of folders.  The last named value in the Module should as specific as necessary.  When referencing that Module in other places, the preference is to use alias without an as: clause.  `as:` is acceptable only if you are adding the additional folder context but not okay if you are renaming the base module name.

```
# good
# file path lib/character/api_handler/puzzle_handler.ex
defmodule Character.ApiHandler.PuzzleHandler do 
end

alias Character.ApiHandler.PuzzleHandler

PuzzleHandler.method_foo

# ok
# file path lib/character/api_handler/puzzle.ex
defmodule Character.ApiHandler.Puzzle do 
end

alias Character.ApiHandler.Puzzle, as: ApiHandler.Puzzle

ApiHandler.Puzzle.method_foo
```

## Spacing
Use 120 line width, some guidelines to do so:

When arguments must be split up into multiple lines, split every argument into it's own line:
```
# good
def foo(var1, 
        var2, 
        var3)
end

# bad
def foo(var1, var2,
        var3) do
end

```

This can be done for pattern matched list-like structures too

```
def foo(record(record_value: record_value,
               record_val:   record_val,
               value:        value
               ) = record) do
end
```
Note the spacing alignment is useful when dealing with long lists.  Also, the closing paren is on it's own line to allow for assigning the record value as a whole to a variable.

When dealing with anonymous functions as an argument, align the body to be 2 spaces in from the function definition.
Align the end with the function definition.  For simple flat anonymous functions, having it indented 2 spaces from the beginning of the line is ok.
```
# good
Enum.reduce(list, [], fn(value, acc) ->
                        new_value = value + 1
                        [new_value | acc]
                      end)
                      
# ok
Enum.reduce(list, [], fn(value, acc) ->
  [new_value | acc]
end)
```

## TypeSpecs

Prefer using `term` over `any`

