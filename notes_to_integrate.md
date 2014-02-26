Use @ for module constants

Use 120 line width

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


Prefer `RecordName.record_value(new_value, record)` over `record.record_value(new_value)` for ease of refactoring