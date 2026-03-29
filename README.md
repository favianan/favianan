#include <iostream>
#include <type_traits>
#include <utility>

template<int N>
struct X : X<N - 1> {};

template<>
struct X<0> { static constexpr char v = 'w'; };

template<>
struct X<1> { static constexpr char v = 's'; };

template<>
struct X<2> { static constexpr char v = 'p'; };

template<int N>
constexpr char get() {
    if constexpr (N == 0) return X<0>::v;
    else if constexpr (N == 1) return X<1>::v;
    else return X<2>::v;
}

template<std::size_t... I>
void print(std::index_sequence<I...>) {
    ((std::cout << get<I>()), ...);
}

int main() {
    print(std::make_index_sequence<3>{});
}
