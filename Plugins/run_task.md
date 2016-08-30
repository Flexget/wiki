# Run Task

| Option | Default | Description |
| --- | --- | --- |
| when | always | Specify when other task is executed. Possible values are `accepted`, `rejected`, `failed`, `aborted`, `always`.|
| task | -- | Name of task to be executed

#### Example

```yaml
run_task:
  when: accepted
  task: another-task-to-be-executed
```
