Testing
=======

Frameworks
----------

We will be consistent about the testing frameworks that we use. Ensuring that every developer can efficiently read every spec sets a low barrier to entry for contribution, and can behave as short-term documentation for common behaviors.

If you are the first developer to work in a language, it is your responsability to choose the testing framework that elos will use for projects in that language. Preferred frameworks will:

- have an [RSpec](http://rspec.info/)-style syntax
- be capable of both unit and integration testing
- be runnable from the command line
- work with a CI platform such as [Travis](https://travis-ci.org/first_sync)
- be trivial to set up, in order to save time with multi-platform testing

| Language | Framework                                |
| -------- | :-------------------------------------:  |
| Go       | [Ginkgo](https://github.com/onsi/ginkgo) |
| Swift    | [Quick](https://github.com/Quick/Quick)  |

Tests
-----

### `it` statements

An `it` statement should read like a sentence in the simple present tense:

```ruby
it 'reads like a sentence' { ... }
it 'works like a charm' { ... }
it 'has an actual description of what it is doing' { ... }
```

### `describe` blocks

Use a `describe` block to group tests by subject

```ruby
describe 'User' do
  describe '.top' do
    it 'returns the top n users with the top score' { ... }
    it 'returns all users when n > User.count' { ... }
  end
end
```

### `context` blocks

Use a `context` block to group tests with similar setups:

```ruby
context 'when logged in' do
  before { log_in }
  it { is_expected.to respond_with 200 }
end
context 'when logged out' do
  it { is_expected.to respond_with 401 }
end
```
