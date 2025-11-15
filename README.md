# Wt-Ann
 # домашняя работа №2 (9.10)
 
  # 1.
l, r = map(int, input().split())

powers_of_two = []
current_power = 1

# Find the smallest power of two that is >= l
# This loop efficiently brings current_power up to at least l
while current_power < l:
    current_power *= 2

# Collect all powers of two up to r
while current_power <= r:
    powers_of_two.append(str(current_power))
    # Optimization: Prevent potential infinite loop or unnecessary large number generation
    # if r is very large and current_power * 2 would exceed r's practical limits
    # or if current_power is already half of r, the next multiplication will exceed r
    if current_power > r // 2: 
        break
    current_power *= 2

print(' '.join(powers_of_two))


  # 2.
import math

n = int(input())

divisors = set() # Using a set to automatically handle unique divisors

for i in range(1, int(math.sqrt(n)) + 1):
    if n % i == 0:
        divisors.add(i)
        divisors.add(n // i)

sorted_divisors = sorted(list(divisors))
print(' '.join(map(str, sorted_divisors)))


  # 3.
year = int(input())

is_leap = False

if (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0):
    is_leap = True

if is_leap:
    print('Да')
else:
    print('Нет')


  # 4.
k, l, m, n = map(int, input().split())

is_threatened = False

# Check if in the same row or column
if k == m or l == n:
    is_threatened = True
# Check if in the same diagonal
elif abs(k - m) == abs(l - n):
    is_threatened = True

if is_threatened:
    print('Да')
else:
    print('Нет')


  # 5.
k = int(input())

h = k // 3600
m = (k % 3600) // 60

print(f"{h} hours {m} minutes")


  # 6.
n = int(input())

for i in range(n):
    # Calculate number of spaces and asterisks for each row
    num_spaces = n - 1 - i
    num_asterisks = 2 * i + 1
    
    # Print the row
    print(' ' * num_spaces + '*' * num_asterisks)


  # 7.
n = int(input())

# Read the first number to initialize min and max
current_num = int(input())
minimum = current_num
maximum = current_num

# Iterate through the remaining n-1 numbers
for _ in range(n - 1):
    current_num = int(input())
    if current_num < minimum:
        minimum = current_num
    if current_num > maximum:
        maximum = current_num

print(f"{minimum} {maximum}")


  # 8.
n = int(input())

# Initialize min1 and min2 with a very large value
# or with the first two numbers if n >= 2
# Since input constraints are -1000 <= ai <= 1000, 1001 is a safe large value.
min1 = 1001 
min2 = 1001 

# Read all numbers and update min1 and min2
for _ in range(n):
    current_num = int(input())
    
    if current_num < min1:
        min2 = min1 # The previous min1 becomes the second minimum
        min1 = current_num # current_num is the new minimum
    elif current_num < min2: # If not smaller than min1, check if smaller than min2
        min2 = current_num
        
print(f"{min1} {min2}")



# домашняя работа №3  (15.10)
  # 1.
n = int(input())
arr = list(map(int, input().split()))

if not arr:
    print()
else:
    max_val = arr[0]
    min_val = arr[0]
    max_idx = 0
    min_idx = 0

    for i in range(1, n):
        if arr[i] > max_val:
            max_val = arr[i]
            max_idx = i
        if arr[i] < min_val:
            min_val = arr[i]
            min_idx = i

    # Swap elements
    arr[max_idx], arr[min_idx] = arr[min_idx], arr[max_idx]

    print(*(str(x) for x in arr))


  # 2.
n = int(input())
arr = list(map(int, input().split()))

if n < 2:
    # Handle cases where there aren't enough numbers to pick two
    print("Not enough numbers to form a pair.")
else:
    arr.sort()

    # Product of the two largest numbers
    prod1 = arr[-1] * arr[-2]

    # Product of the two smallest numbers
    prod2 = arr[0] * arr[1]

    if prod1 > prod2:
        print(arr[-2], arr[-1])
    else:
        print(arr[0], arr[1])


  # 3.
N = int(input())

all_languages = set()  # Languages known by at least one student
common_languages = None  # Languages known by all students

for _ in range(N):
    M_i = int(input())
    current_student_languages = set()
    for _ in range(M_i):
        lang = input()
        current_student_languages.add(lang)

    if common_languages is None:
        common_languages = current_student_languages
    else:
        common_languages.intersection_update(current_student_languages)

    all_languages.update(current_student_languages)

# Output languages known by all students
print(len(common_languages))
for lang in sorted(list(common_languages)):
    print(lang)

# Output languages known by at least one student
print(len(all_languages))
for lang in sorted(list(all_languages)):
    print(lang)


  # 4.
n = int(input())

sales_data = {}

for _ in range(n):
    line = input().split()
    customer = line[0]
    product = line[1]
    quantity = int(line[2])

    if customer not in sales_data:
        sales_data[customer] = {}
    
    sales_data[customer][product] = sales_data[customer].get(product, 0) + quantity

# Output the results
for customer in sorted(sales_data.keys()):
    print(f"{customer}:")
    for product in sorted(sales_data[customer].keys()):
        print(f"  {product} {sales_data[customer][product]}")


  # 5.
from collections import defaultdict

n = int(input())
word_counts = defaultdict(int)

for _ in range(n):
    line = input().split()
    for word in line:
        word_counts[word] += 1

# Create a list of tuples (count, word) for sorting
# Use -count for descending order of frequency, and word for ascending lexicographical order
sorted_words = []
for word, count in word_counts.items():
    sorted_words.append((-count, word))

# Sort the list of tuples
sorted_words.sort()

# Print the words
for count, word in sorted_words:
    print(word)


  # 6.
n = int(input())

# Initialize the set of all possible numbers from 1 to n
possible_numbers = set(range(1, n + 1))

while True:
    line = input()
    if line == 'HELP':
        break

    # Convert Beatrice's numbers into a set
    guessed_set = set(map(int, line.split()))
    
    answer = input() # Read August's answer (YES/NO)

    if answer == 'YES':
        # If YES, the number must be in the guessed set
        possible_numbers.intersection_update(guessed_set)
    elif answer == 'NO':
        # If NO, the number cannot be in the guessed set
        possible_numbers.difference_update(guessed_set)

# Print the remaining possible numbers, sorted
print(*(sorted(list(possible_numbers))))


  # 7.
n = int(input())
arr = list(map(int, input().split()))

# Use a dictionary to store counts of each element
counts = {}
for x in arr:
    counts[x] = counts.get(x, 0) + 1

# Iterate through the original array to print elements that appear only once
result = []
for x in arr:
    if counts[x] == 1:
        result.append(str(x))

print(' '.join(result))



# домашняя работа №4   (21.10)



# домашняя работа №5  (14.10)
