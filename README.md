Itertools Idioms
================

Useful programming idioms with Python itertools.

Usage:

    >>> from itertools_idioms import idioms
    # Select keys using variable constraints

    >>> import operator
    >>> prices = {'cake': 50, 'bread': 20, 'pie': 100}
    >>> constraints = {'cake': (operator.lt, 60), 'bread': (operator.le, 20), 'pie': (operator.lt, 80)}
    >>> list(idioms.select(prices,constraints))
    ['cake', 'bread']

    # second option - supply your own constraing mapping to functions
    >>> constraints = {'cake': ('less', 60), 'bread': ('less', 30), 'pie': ('lessorequal', 80)}
    >>> cmap = {'less': operator.lt, 'lessorequal': operator.le}
    >>> list(idioms.select(prices,constraints, cmap=cmap))  
    ['cake', 'bread']

    # best option - use default operator module mapping for comparison constraints.
    >>> constraints = {'cake': ('<', 60), 'bread': ('<=', 20), 'pie': ('<', 80)}
    >>> list(idioms.select(prices,constraints, use_operator=True))
    ['cake', 'bread']

    # Use select2 if the conditions are directly expressed as functions
    >>> constraints = {'cake': lambda x: x<60,
    ...                'bread': lambda x: x<=20,
    ...                'pie': lambda x: x<80 }
    >>> list(idioms.select2(prices, constraints))
    ['cake', 'bread']
    
    # Use 'call' to return iterables from callables which vary
    # in output when called at different times. Use optional
    # 'times' and 'filter' arguments to control the output.
    
    # Return upto 10 random numbers between 1 and 100
    >>> list(idioms.call(random.choice, range(10), times=10))
    [8, 8, 1, 4, 4, 6, 7, 3, 9, 2]

    # Return upto 10 random numbers between 1 and 100 which
    # are multiples of 3
    >>> list(idioms.call(random.choice, range(100), times=10, filter=lambda x: x%3==0))
    [93, 72, 63]

    # Random streams - infinite and constrained
    
    # Infinite random stream from your iterable
    >>> for i in idioms.random_stream(iterable): print i

    # Specific random streaming functions
    # This would keep going forever
    >>> for i in idioms.random_alphabets(): print i

    # This is constrained and stops when it encounters W
    >>> list(idioms.random_alphabets(sentinel='W'))
    ['i', 'o', 'z', 'y', 'd', 'Z', 'Y', 's', 'S', 'O', 'Q']

    # Infinite generator of random digits    
    >>> idioms.random_digits()
    <itertools.imap object at 0xa12f76c>
    
    # Would stop when encountering 8
    >>> list(idioms.random_digits(sentinel=8))
    [4, 2, 3, 2, 9, 5, 9, 3, 7, 7, 5, 5, 3, 5]

    >>> 'More coming soon!'
    'More coming soon!'
