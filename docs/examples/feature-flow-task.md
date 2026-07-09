# Example: Task Feature Flow

This is a generic feature-flow example for a desktop task list.

## User intent

The user marks a task as completed.

## Flow

```text
TaskListView -> CompleteTaskCommand -> TaskListViewModel.CompleteTaskAsync -> CompleteTaskUseCase -> ITaskGateway -> LocalTaskGateway or GraphTodoGateway -> CompleteTaskResult -> TaskListViewState
```

## Application model

```csharp
namespace ExampleApp.Application.Tasks;

public sealed record CompleteTaskRequest(string TaskId);

public abstract record CompleteTaskResult
{
    public sealed record Success(string TaskId) : CompleteTaskResult;
    public sealed record NotFound(string TaskId) : CompleteTaskResult;
    public sealed record PermissionDenied : CompleteTaskResult;
    public sealed record NetworkUnavailable : CompleteTaskResult;
}
```

## Boundary rule

The ViewModel does not know whether the task is completed through local storage, Graph To Do, or another external API. That decision is behind `ITaskGateway` and its Infrastructure implementation.
