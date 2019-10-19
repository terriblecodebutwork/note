## define a subscribe function of a database model/context topic

```ex
  @topic inspect(__MODULE__)

  @spec subscribe :: :ok | {:error, any}
  def subscribe do
    Phoenix.PubSub.subscribe(Demo.PubSub, @topic)
  end
  
  
  # make notify when got success result
  defp notify_subscribers({:ok, result}, event) do
    Phoenix.PubSub.broadcast(Demo.PubSub, @topic, {__MODULE__, event, result})
    Phoenix.PubSub.broadcast(Demo.PubSub, @topic <> "#{result.id}", {__MODULE__, event, result})
    {:ok, result}
  end

  defp notify_subscribers({:error, reason}, _event), do: {:error, reason}
```
