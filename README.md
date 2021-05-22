# plf::nanotimer
A simple C++ 03/11/etc timer class for ~microsecond-precision cross-platform benchmarking. The implementation is as limited and simple as possible to afford the lowest amount of overhead.


Use as follows:

	plf::nanotimer timer;


	timer.start()

	// Do something here

	double results = timer.get_elapsed_ns();
	std::cout << "Timing: " << results << " nanoseconds." << std::endl;


	timer.start(); // "start" has the same semantics as "restart".

	// Do something else

	results = timer.get_elapsed_ms();
	std::cout << "Timing: " << results << " milliseconds." << std::endl;


	timer.start()

	plf::microsecond_delay(15); // Delay program for 15 microseconds

	results = timer.get_elapsed_us();
	std::cout << "Timing: " << results << " microseconds." << std::endl;



Timer member functions:
=======================

void start(): start or restart timer

double get_elapsed_ns(): get elapsed time in nanoseconds

double get_elapsed_us(): get elapsed time in microseconds

double get_elapsed_ms(): get elapsed time in milliseconds



Non-member functions:
=====================

void plf::millisecond_delay(double x): delay the program until x milliseconds have passed

void plf::microsecond_delay(double x): delay the program until x microseconds have passed

void plf::nanosecond_delay(double x): delay the program until x nanoseconds have passed



Timer 'pausing':
================

I determined that a 'pause'-style function would add too much complexity to the class for simple benchmarking, which in turn might interfere with performance analysis, so if you need a 'pause' function do something like this:

	plf::nanotimer timer;


	timer.start()
	// Do something here
	double results = timer.get_elapsed_ns();

	// Do something else - timer 'paused'

	timer.start()

	// Do stuff

	results += timer.get_elapsed_ns();

	std::cout << "Timing: " << results << " nanoseconds." << std::endl;
