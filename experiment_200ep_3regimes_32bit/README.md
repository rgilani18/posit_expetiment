# Separate 32-bit GCN Experiment

This directory is an isolated 32-bit counterpart to `experiment_200ep_3regimes`.
It does not modify or reuse that experiment's source files or result files.

The experiment uses the same Cora data, initial weights, seed, model dimensions,
dropout, learning rates, weight decay, evaluation masks, and three training
regimes as the original experiment. Only the arithmetic types change:

- FP32: `sw::universal::cfloat<32, 8>`
- Posit32: `sw::universal::posit<32, 2>`

The three programs are:

- `src/cpp/train_2layer_gd_32bit.cpp`
- `src/cpp/train_2layer_pure32_adam_32bit.cpp`
- `src/cpp/train_2layer_double_adam_32bit.cpp`
- `src/cpp/evaluate_3regimes_numerical_accuracy_32bit.cpp`

Each accepts an optional epoch count; the default is 200. From this directory,
compile with a C++20 compiler and the bundled Universal headers:

```text
g++ -std=c++20 -O2 -Iuniversal/include -Iuniversal/include/sw src/cpp/train_2layer_gd_32bit.cpp -o train_gd_32bit
g++ -std=c++20 -O2 -Iuniversal/include -Iuniversal/include/sw src/cpp/train_2layer_pure32_adam_32bit.cpp -o train_pure32_adam_32bit
g++ -std=c++20 -O2 -Iuniversal/include -Iuniversal/include/sw src/cpp/train_2layer_double_adam_32bit.cpp -o train_double_adam_32bit
g++ -std=c++20 -O2 -Iuniversal/include -Iuniversal/include/sw src/cpp/evaluate_3regimes_numerical_accuracy_32bit.cpp -o evaluate_32bit
```

Run an executable from this directory so its relative `data`, `checkpoints`,
and `results` paths resolve correctly. For example:

```text
train_gd_32bit.exe 200
```
