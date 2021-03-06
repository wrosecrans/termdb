# TermDb [![Build Status](https://travis-ci.org/agauniyal/termdb.svg?branch=master)](https://travis-ci.org/agauniyal/termdb) [![codecov](https://codecov.io/gh/agauniyal/termdb/branch/master/graph/badge.svg)](https://codecov.io/gh/agauniyal/termdb)

Terminfo parser for modern c++. **[Docs](https://github.com/agauniyal/termdb/blob/master/docs/info.md)**.

```cpp
#include "termdb.hpp"
#include <iostream>

using namespace tdb;

int main()
{
	TermDb parser;
	auto result = parser.parse("xterm");

	if (result) {
		auto name = parser.getName();
		auto b    = parser.get(bin::has_meta_key);
		auto n    = parser.get(num::columns);
		auto s    = parser.get(str::enter_bold_mode);

		std::cout << "\n"
		          << "Name: " << name << "\n"
		          << "Has Meta Key: " << std::boolalpha << b << "\n"
		          << "Number of columns: " << n.value_or(24) << "\n"
		          << "Bold Mode on: " << s << "I should be BOLD!"
		          << "\n";
	} else {
		std::cerr << "Couldn't parse terminfo database\n";
	}
}
```
