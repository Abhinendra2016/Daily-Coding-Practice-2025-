# Problem 2115: Find All Possible Recipes from Given Supplies

You have information about `n` different recipes. You are given a string array `recipes` and a 2D string array `ingredients`. The `i-th` recipe has the name `recipes[i]`, and you can create it if you have all the needed ingredients from `ingredients[i]`. A recipe can also be an ingredient for other recipes.

You are also given a string array `supplies` containing all the ingredients that you initially have.

Return a list of all the recipes that you can create. You may return the answer in any order.

## Example 1:

**Input**:
recipes = ["bread"] ingredients = [["yeast","flour"]] supplies = ["yeast","flour","corn"]


**Output**:

["bread"]


## Example 2:

**Input**:

recipes = ["bread","sandwich"] ingredients = [["yeast","flour"],["bread","meat"]] supplies = ["yeast","flour","meat"]


**Output**:
["bread","sandwich"]


## Example 3:

**Input**:


recipes = ["bread","sandwich","burger"] ingredients = [["yeast","flour"],["bread","meat"],["sandwich","meat","bread"]] supplies = ["yeast","flour","meat"]



**Output**:

["bread","sandwich","burger"]


## Solution

```python
class Solution:
    def findAllRecipes(
        self,
        recipes: list[str],
        ingredients: list[list[str]],
        supplies: list[str],
    ) -> list[str]:
        ans = []
        supplies = set(supplies)
        graph = collections.defaultdict(list)
        inDegrees = collections.Counter()
        q = collections.deque()
        
        # Build graph and in-degree count
        for i, recipe in enumerate(recipes):
            for ingredient in ingredients[i]:
                if ingredient not in supplies:
                    graph[ingredient].append(recipe)
                    inDegrees[recipe] += 1
        
        # Recipes with zero in-degree can be made directly
        for recipe in recipes:
            if inDegrees[recipe] == 0:
                q.append(recipe)
        
        # Topological sort (Kahn's Algorithm)
        while q:
            u = q.popleft()
            ans.append(u)
            for v in graph[u]:
                inDegrees[v] -= 1
                if inDegrees[v] == 0:
                    q.append(v)
        
        return ans
```
<h2>Time Complexity</h2> O(N + E), where N is the number of recipes and E is the total number of ingredient dependencies across all recipes.<br>
 <h2>Space Complexity</h2> O(N + E) for storing the graph and in-degree counts.<br>
  <h2>Explanation</h2> 
  We model the problem as a directed graph where an edge points from an ingredient to a recipe. We track how many ingredients are needed before a recipe can be made (in-degree). We start from supplies (given ingredients) and recipes that can already be made (in-degree = 0), then process each node while reducing in-degrees of dependent recipes. If a dependent recipe's in-degree becomes zero, it can also be made. 