# cubit2cubit

A Flutter tutorial application by Your Dev Edge.

## Description

This is a series of tutorials that focuses on State and State Management using the Bloc Package.

This is one of several "Overview" applications that demonstrate the basics of Cubit/Bloc.

This app will demonstrate Cubit to Cubit communication using StreamSubscription.


Notes:

Unlike initial or dispose, when using:
@override
  Future<void> close() {
    colorSubscription.cancel();
    return super.close();
  }

Put what you want to happen before the call to super.close.


This is the stream from X to Y part:

In counter_cubit.dart:

CounterCubit({
  final ColorCubit colorCubit;
  late final StreamSubscription colorSubscription;

  CounterCubit({
    required this.colorCubit,
  }) : super(CounterState.initial()) {
    colorSubscription = colorCubit.stream.listen((ColorState colorState) {

In main.dart:

MultiBlocProvider(
      providers: [
        BlocProvider<ColorCubit>(
          create: (context) => ColorCubit(),
        ),
        BlocProvider<CounterCubit>(
          create: (context) => CounterCubit(     <--------
            colorCubit: context.read<ColorCubit>(),  <--------
          ),
        ),