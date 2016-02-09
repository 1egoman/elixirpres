# &nbsp;
# Why Elixir is
# my new favorite language
---
# &nbsp;
# It's functional.
---
# &nbsp;
# It's Performant.
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Final results from Phoenix channel benchmarks on 40core/128gb box. 2 million clients, limited by ulimit<a href="https://twitter.com/hashtag/elixirlang?src=hash"> #elixirlang</a> <a href="https://t.co/6wRUIfFyKZ">pic.twitter.com/6wRUIfFyKZ</a></p>&mdash; Chris McCord (@chris_mccord) <a href="https://twitter.com/chris_mccord/status/659430661942550528">October 28, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
---
<img src="https://pbs.twimg.com/media/CSbEsTiW0AARBzf.png" style="height: 600px;" />
---
# &nbsp;
# Pattern matching, guards, and recursion are amazing. 
---
# &nbsp;
# Multi-threading is easy.
---
# &nbsp;
# Don't believe me?
---
## Javascript
```javascript
function fib(n) {
  if (n === 0) {
    return 0;
  } else if (n === 1) {
    return 1;
  } else if (Number.isFinite(n)) {
    return fib(n-1) + fib(n-2);
  } else {
    return null;
  }
}
```
---
## Elixir
```elixir
def fib(0), do: 0
def fib(1), do: 1
def fib(n) when is_integer(n) do
  fib(n-1) + fib(n-2)
end
def fib(_), do: nil
```
---
## Elixir, multithreaded
```elixir
defmodule Stack do
  use GenServer

  def handle_call(:pop, _from, [head | tail]) do
    {:reply, head, tail}
  end

  def handle_cast({:push, item}, state) do
    {:noreply, [item | state]}
  end
end

{:ok, pid} = GenServer.start_link(Stack, [:hello])
GenServer.call(pid, :pop)
#=> :hello
GenServer.cast(pid, {:push, :world})
#=> :ok
GenServer.call(pid, :pop)
#=> :world

# I'll do something else
for i <- 1..10, do: IO.puts(i)
```
---
# &nbsp;
# Phoenix &#8776; Rails, but with channels.
