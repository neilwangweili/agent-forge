# 从两天到两小时：我们的 Scrum + XP + AI 实践

你是否经历过这样的场景：需求在开发过程中不断变化，几个月的努力最终发现做的不是用户真正想要的？代码质量参差不齐，一个人写的代码只有他自己看得懂？测试覆盖率低，每次改动都提心吊胆怕引入新 bug？部署流程繁琐，一个小功能要等几周才能上线？

我们也经历过。直到我们采用了 Scrum + XP + AI 的组合拳，一切都变了。一个功能从需求到上线，从过去的两天缩短到现在的两小时左右。代码质量稳定，测试覆盖率 100%，部署全自动化。最重要的是，我们不再害怕变化，反而能快速响应市场需求。

这不是理论，而是我们的实践经验。现在我就把它分享给大家。

## 第一章：我们为什么选择 Scrum + XP

### 传统方式的痛点

在采用 Scrum + XP 之前，我们的开发流程是典型的瀑布式。

需求阶段花几周收集需求，设计阶段画几周架构图，然后开发几个月，最后测试几周。问题在于，当我们终于交付产品时，市场已经变了，用户需求也变了。

更糟糕的是变更成本。如果在需求阶段发现问题，变更成本很低。在开发阶段发现，变更成本会高一点。在测试阶段发现，变更成本还行。在生产环境发现，变更成本可能就非常巨大来。这种高昂的变更成本让我们对需求变化非常排斥，总是试图在开始前就把所有需求定死。可是这咋可能呢？

代码质量也是大问题。大佬写出高质量代码，但新手的代码经常出问题。测试在开发完成后进行，发现问题时修复成本已经很高。技术债务逐渐累积，系统越来越难维护。

### Scrum + XP 如何解决问题

所以，我们引入了 Scrum + Xp 来解决这个问题。Scrum 提供了敏捷的项目管理框架，用 1 - 2 周的 Sprint 替代数月的开发周期。每个 Sprint 结束时,我们有一个可工作的增量演示给客户，收集反馈。需求变更不再是灾难，而是正常的、可管理的过程。PO可以根据市场反馈随时调整优先级。

Standish Group 2020 年的 CHAOS 报告显示，Scrum/Agile 项目的成功率是 42%，瀑布项目只有 13%——成功率提升 3 倍。更重要的是，瀑布项目的失败率高达 59%，而 Agile 只有 11%。

再谈Xp，Xp是极限编程，提供了卓越的工程实践。TDD 确保代码质量，Pair Programming 促进知识共享，Continuous Integration 早期发现问题。Microsoft 和 IBM 的联合研究（2008）显示，TDD 使缺陷密度降低 40-80%，测试覆盖率从 30-50% 提升到 90% 以上。虽然初期开发时间增加 15-35%，但维护成本的降低远超这个投入。

这不是抽象的理论。Danske Bank 采用 Agile 后，交付时间从 14 个月缩短到 9 个月，更重要的是，首次交付只需 4 个月——相比传统方式缩短 71%。投资回报期大大提前。

### 为什么是 Scrum + XP，而不是单独使用

Scrum 解决做什么和何时做的问题，但不关心怎么做。如果没有好的工程实践，Scrum 也可能失败，因为快速交付低质量的代码只会加速项目崩溃。

XP 提供了卓越的工程实践，但缺乏项目管理框架。没有 Scrum 的迭代节奏和反馈机制，很难确保团队在构建正确的产品。

所以经过研究发现，把 Scrum 和 XP 一起用比较好，Scrum 提供项目管理框架，XP 提供工程实践保障。两者互补，形成从需求到部署的完整敏捷开发方法论。

## 第二章：我们的实践流程

### 2.1 从一句话需求到可工作的功能

我们的实践流程包括五个步骤：需求分析 → Sprint 计划 → TDD 编码 → 端到端测试 → 自动化部署。每个 Sprint 的输出是一个可工作的增量，经过完整测试，可以直接部署到生产环境。

#### 第一步：领域建模 + 用户故事地图

在 Sprint Planning 之前，我们会做领域建模。我们用 Event Storming 的方式：团队和产品经理聚在一起，在白板上贴便利贴，通过四色建模的方式来完成领域建模。

通过这个过程，我们识别出核心的领域概念：实体（Entity）、值对象（Value Object）、聚合（Aggregate）、边界上下文（Bounded Context）。这些概念会直接体现在代码中——我们用业务术语写代码，而不是 data1、data2 这种无意义的名字。

用户故事地图帮助我们从用户视角组织需求。横向是用户旅程（从左到右），纵向是优先级（从上到下）。这让我们清楚地看到产品全貌，识别出 MVP（最小可行产品）和后续版本的范围。

#### 第二步：编写用户故事和验收标准

用户故事是种拆分细化的需求，每个用户故事都要遵循标准格式：**As a [角色], I want [功能], So that [价值]**

例如：As a customer, I want to search products by category, So that I can quickly find what I need。

这样写的好处是三要素集齐，需求非常精准、明确，符合 INVEST 和 SMART 原则。

在用户故事中，我们定义了很多AC（故事完成的标准），采用 Given-When-Then 格式：

```
Given I am on the product search page
When I select "Electronics" category and click "Search"
Then I should see all products in the Electronics category
And the products should be sorted by relevance
```

AC 是我们编写测试的依据。每个 AC 对应一个或多个自动化测试。同时也对应了端到端测试的测试用例。清晰的 AC 让开发者知道要实现什么，测试者知道要验证什么。

#### 第三步：TDD

这是我们编码的核心实践。我们不是先写代码再写测试，而是先写测试，再写代码，让代码最快速地修复测试。然后再去重构，不停循环直到 AC 完成。

用户故事描述了为什么需要这个功能，AC 描述了功能该如何实现，TDD 负责如何用测试验证编码已实现，三者合一，让编码能贯穿整个上下文。

我们遵循了测试金字塔原则，通过构建了大量单元测试、适量集成测试及与 AC 一一匹配的端到端测试，把整个项目的功能全部覆盖住，构建完备的安全网。

比方说，对于搜索产品这个需求，

**单元测试**（JUnit）测试单个方法的行为：

```java
@Test
void productShouldMatchCategory() {
    Product product = new Product("Laptop",
        new Category("Electronics"),
        new Money(999, "USD"));

    assertThat(product.isInCategory(new Category("Electronics"))).isTrue();
    assertThat(product.isInCategory(new Category("Books"))).isFalse();
}
```

**集成测试**（JUnit + TestContainers）测试与数据库的交互：

```java
@Test
void shouldSearchProductsByCategory() {
    Category category = new Category("Electronics");
    List<Product> results = searchService.search(
        new SearchCriteria(category));
    assertThat(results).isNotEmpty();
    assertThat(results).allMatch(p -> p.isInCategory(category));
}
```

**端到端测试**（Cypress）模拟真实用户操作：

```javascript
test('search products by category', async () => {
    await page.goto('/search');
    await page.selectOption('#category', 'Electronics');
    await page.click('#search-button');

    const products = await page.$$('.product-item');
    expect(products.length).toBeGreaterThan(0);
});
```

对于每个功能，我们遵循**红-绿-重构**循环。第一步是“红”，写一个失败的测试，比如测试 `ProductService` 的 `search` 方法应该返回指定分类的产品。运行测试，测试失败，显示红色。

第二步是“绿”，写最少的代码让测试通过。实现 `search` 方法，查询数据库，返回结果。运行测试，测试通过，显示绿色。

第三步是“重构”，在测试的保护下改进代码质量，消除重复，改善命名，提取方法。运行测试，确保仍然通过。

每个循环很小，可能只需几分钟。小步前进降低了认知负担，让我们可以专注于一个小目标。

#### 第四步：运用 Smart Domain 和小对象模式

这是我们代码质量提升的关键，于架构实践多次后发现的最优解。

以前我们写的代码是这样的（贫血模型）：

```java
public class Order {
    private String id;
    private BigDecimal amount;
    private String status;
    // 只有 getters 和 setters
}

public class OrderService {
    public void approveOrder(Order order) {
        if (order.getAmount().compareTo(BigDecimal.ZERO) <= 0) {
            throw new IllegalArgumentException("Invalid amount");
        }
        if (!"PENDING".equals(order.getStatus())) {
            throw new IllegalStateException("Order not pending");
        }
        order.setStatus("APPROVED");
    }
}
```

问题在哪？验证逻辑在服务层，容易重复。Order 对象是被动的数据容器，不负责维护自己的一致性。几个月后，同样的验证逻辑散落在十几个地方，每次修改规则都要改十几处。

这里对应的是重构手则中的霰弹式修改，这也是非常常见的坏味道。

现在我们这样写（富领域模型）：

```java
public class Order {
    private final OrderId id;
    private final Money amount;
    private OrderStatus status;

    public Order(OrderId id, Money amount) {
        this.id = id;
        this.amount = amount;
        this.status = OrderStatus.PENDING;
    }

    public void approve() {
        if (!status.canTransitionTo(OrderStatus.APPROVED)) {
            throw new IllegalStateException(
                "Cannot approve order in status: " + status);
        }
        this.status = OrderStatus.APPROVED;
    }
}

public class OrderService {
    public void approveOrder(Order order) {
        order.approve(); // 业务逻辑在 Order 中
    }
}
```

业务规则集中在 `Order` 中，没有重复。Order 负责维护自己的一致性，服务层只需调用领域对象的方法。当业务规则变化时，我们只需改一个地方。

再举个例子，以前我们到处用 String：

```java
public class User {
    private String email;
    private String name;

    public User(String email, String name) {
        if (!email.contains("@")) {
            throw new IllegalArgumentException("Invalid email");
        }
        this.email = email;
        this.name = name;
    }

    public void sendEmail(String email, String message) { 
        // ... 
    }
}
```

这就有问题了。因为 email 和 name 都是 String，容易传错。验证逻辑分散在多处。IDE 没法帮我们检查类型错误，同时也产生了无数的重复代码。

有人说用Utils，Utils是反面向对象设计，能不用就不用。 我们用 Value Objects：

```java
public class Email {
    private final String value;

    public Email(String value) {
        if (!isValid(value)) {
            throw new IllegalArgumentException("Invalid email: " + value);
        }
        this.value = value;
    }

    private static boolean isValid(String email) {
        return email.matches("^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$");
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Email email = (Email) o;
        return value.equals(email.value);
    }

    @Override
    public int hashCode() {
        return value.hashCode();
    }
}

public class User {
    private final Email email;
    private final String name;

    public User(Email email, String name) {
        this.email = email;
        this.name = name;
    }

    public void sendEmail(Email recipient, String message) { 
        // ...
    }
}
```

优势极大。首先是类型安全：编译器会阻止你把 email 传给 name 参数，在编译阶段就能发现错误。其次是验证集中，所有的验证逻辑只需要在 Email 构造函数中实现一次，不会有任何遗漏。

另一个优势是业务语义清晰：当看到 `Email` 类型时，立刻就知道这是邮箱，看到 `Money` 类型时，就知道这是金额和货币的组合，非常符合业务语义，生动形象。

最后是易于重构，如果需要修改 email 的格式规则，你只需要修改 `Email` 类的验证逻辑，所有使用这个类的地方都会自动应用新规则。

我们大量使用 Value Objects，把每一个具有业务语义的基本类型全部封装。

再看看实际收益如何，我们统计了一下，采用 Smart Domain 和小对象模式后，我们的代码质量明显提升。Bug 数量大幅减少，因为类型安全机制避免了大量参数传错的低级错误。重构变得更安全，完整的测试套件加上类型系统给我们双重保障，让我们可以放心地改进代码结构。新人上手速度加快，代码自文档化的特性让他们看到类型就能理解含义，不需要翻阅大量文档。维护成本显著降低，业务规则集中在领域对象中，修改一处即可生效，不需要在多个地方重复修改。

### 第五步： CI / CD

每次代码提交，CI 服务器就自动进行端到端测试、编译和部署，整个流程完全自动化。每次提交相当于做一次回归测试。在测试那章说了，每个端到端测试都对应一个 AC，这对测试人员是非常友好的。

## 第三章：AI 如何改变游戏规则

集成 AI 让项目研发效率产生质的飞跃。我来分享一下实际情况。

接入AI后，一句话就可以从需求直达生产部署。过去往往要研发两天，现在只需要半个小时左右，时间缩短了 96% ，成本大概需要5美元（token消耗）。这怎么能不让人心动？妥妥的降本增效典型。

我们用的是Multi-Agent System来实现的。

### 3.1 Multi-Agent System

我们构建了一个 Multi-Agent System（MAS），包含 5 个专门化的 AI agents 和一个协调者：

**Requirements Analyst Agent**（需求分析专家）：它将一句话需求转化为详细的用户故事和验收标准。我们给它一句话需求，它来生成完整的用户故事和AC。

**Domain Modeler Agent**（领域建模专家）：它分析用户故事，识别出领域概念、实体、值对象，进行建模及维护。

**Test Generator Agent**（测试生成专家）：它根据 AC 生成测试代码，生成端到端测试、集成测试、单元测试。

**Code Generator Agent**（代码生成专家）：它根据严格遵循 TDD 原则通过实现测试用例来生成实现代码。

**Reviewer Agent**（代码审查专家）：它审查代码质量、测试覆盖率、安全漏洞，并识别和改进代码坏味道、识别安全漏洞。

**Coordinator**（协调者）：它分解任务，管理依赖，协调这 5 个 agent 干活，然后整合结果并汇报完成。不顺利的情况协调各个 agent 联手解决问题。

实际使用办法就是，给 AI 一句话的需求，它自动的一个个地做任务、跑流程。自动地把需求分析了，把用户故事写了，把 AC 写了，再把测试和代码敲了，然后提交代码去验证了。

### 3.2 人类的角色

与 AI 协同工作时，人类更应该充当项目负责人、架构师之类的角色来更好地人机协同。可以多开几个对话，让每个对话去实现不同的需求，最后人去合代码。

在我们的实践中，人类审查仍然是关键环节。Reviewer Agent 提供初步审查，但架构决策、复杂业务逻辑、安全关键代码必须由人类审查。

初级开发者受益最大。AI 作为导师和助手，帮助他们学习最佳实践、避免常见错误。研究显示，经验较少的开发者使用 AI 工具时生产力提升更显著。

### 3.3 挑战和建议

AI 不是银弹。我们遇到过挑战。首先是 AI 理解复杂业务逻辑有上限，对于简单、标准的需求，AI 表现出色，但面对复杂、领域特定的需求时，可能会误解意图。所以这就是 MAS 的重要性。它让五个 Agent 分别关注不同的方向，使用 Agent 产物来进行流程的交替流转，降低 AI 的上下文。

软件里有面向对象的几大原则这么个概念，它们其实都在讲一件事，就是分离关注。对 AI 来讲，分离关注也是必要的，能让 AI 的表现更加优秀。

还有个问题生成代码质量不稳定的问题，质量很大程度上取决于提示词（prompt）以及现有仓库代码的质量，模糊的提示词只会导致模糊的代码，这也是重构的价值所在。

## 第四章：如何开始

我想把这套方法告诉你，并且告诉你如何开始。

### 4.1 分阶段实施

不要试图一次性改变所有事情。我们的经验是分三个阶段：

**第一阶段：引入 Scrum 框架**

你要先组建个跨职能团队，规模保持在 3-9 人之间。然后去请一个 Scrum Master，让他去盯着团队 Scrum执行。

这个阶段的重点是建立迭代节奏和反馈机制，先让流程跑起来。

这个阶段一般就两个月时间。

**第二阶段：引入 XP 工程实践及 AI**

当团队适应了 Scrum 的节奏后，开始引入 XP 的工程实践。从新功能开始实践 TDD，然后再去给过往功能补测试。同时建立 CI 管道，至少要做到每次代码提交时自动构建和运行测试，及时发现问题。在新编写的代码中应用 Smart Domain 和小对象模式，让团队通过实践感受这些模式的好处。

这个阶段的重点是提升代码质量，但不要期望立即见效。

同时，引入 AI 辅助。

AI 辅助这方面，琢磨琢磨 AI 提示词是比较关键的，研究怎么写，才能去生成上述6个智能体，让它们能协同交付。

### 4.2 度量和持续改进

建立度量体系，持续改进。在效率方面，去追踪 Sprint 速度，也就是每个 Sprint 完成的故事点数来用来预测团队产能。追踪交付周期去观测团队效率。

重视回顾会的作用，回顾会往往能发现不少问题，致力于团队改进成长，持续优化。

## 结语：拥抱变化，持续改进

从两天到两小时，从混乱无序到井然有序，从恐惧变化到拥抱变化，这就是 Scrum + XP + AI 带给我们的改变。

这是我们实打实的实践，是团队凝聚、持续成长的结果。

如果你也被传统开发方式的痛点困扰，想快速响应市场需求，试试 Scrum + XP + AI 吧。从小处开始，分阶段实施，持续改进。几个月后，你会看到明显的变化。

这是我们的经验，也是我们给你的建议。现在轮到你了。
