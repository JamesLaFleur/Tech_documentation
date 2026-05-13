## OrdersModule

Данный модуль предназначен для получения информации о заказах, рассчета суммы товаров, находящихся в корзине, создание и изменение статуса заказа.

### Для вызова доступны следующие сообщенния:

1. **Получение списка заказов пользователя**

*Route:*
GET_ORDERS_BY_CUSTOMER ('v1/orders/get-list-by-customer')

*Входные данные:*

    | Параметр | Тип данных | Валидация | Описание |
    | --- | --- | --- | --- |
    | mindboxId | string | Обязательный | id mindbox |
    | page | number | Опциональный | Количество страниц |
    | limit | number | Опциональный, мин. знач. - 0 | Кол-во элементов на странице. Если 0, выведутся все элементы |
    | offset | number | Опциональный, мин. знач. - 0 | Отступ от начала. При ненулевом значении можно запрашивать список с 1 страницы |
    | deviceUuid | string | Опциональный | id устройства |

*Функционал:*
Данный метод предназначен для получения списка заказов пользователя.
В данном методе происходит выполнение post-запроса.
Запрос вызывает метод 'Website.4fresh.GetCustomerOrders'.
Если подарочная карта не найдена, выбрасывает исключение NotFoundException.
Результат запроса присваивается переменным status и customerActions.
Если статус запроса не равен 'Success', то выбрасывает исключение 'InternalServerErrorException'.
Возвращает список заказов пользователей или пустой заказ, если список не был получен.

*Выходные данные:*
Возвращает массив объектов с информацией о заказе пользователя:

  | Параметр | Тип данных | Описание |
  | - | - | - |
  | ids | object | Идентификаторы заказа, включая mindboxId |
  | customFields | object | Пользовательские поля заказа |
  | actionTemplate | object | Действия заказа |
  | dateTimeUtc | string  | Дата создания заказа |
  | pointOfContact | object | Информация о точке контакта для заказа |
  | customer | object| Информация о клиенте |
  | order  | object  | Информация о заказе |

Информация о полях объекта `customFields`:

```json
{
    actionType4fresh: string;
    cardsmobileMessageBody: string;
    cardsmobileMessageHeader: string;
    cardsMobileMessageId: string;
    cardsmobileMessageUtmCampaign: string;
    cardsmobileMessageUtmMiddle: string;
    cardsmobileMessageUtmSource: string;
    ecoProject: string;
    greenWaveCanceledTickets: string;
    gwOffpoints: string;
    gwOffTickets: string;
    gwOrderID: string;
    numberOfPoints: string;
    purchase3000r: string;
    refill: string;
    telECOworker: string;
    ticketNumber: string[];
    ticketquantity: string;
    type: string;
    viberDateMessage: string;
    viberIDMessage: string;
    viberStatusMessage: string;
    wADateMessage: string;
    wAIDMessage: string;
    wAStatusMessage: string;
}
```

Информация о полях объекта `actionTemplate`:

```json
{
    systemName: string;
    name: string;
}
```

Информация о полях объекта `pointOfContact`:

```json
{
    ids: {
      externalId: string;
    };
}
```


Информация о полях объекта `customer`:

```json
{
    ids: {
      mindboxId: number;
      publicCodeWA: string;
      synergeticMobileAppID: string;
      telegramID: string;
      vKID: string;
      wAID: string;
      websiteID: string;
      websiteID4fresh: string;
    };
}
```

Информация о полях объекта `order`:

  | Название поля | Тип данных  | Описание |
  | - | - | - |
  | firstPointOfContact| object | Информация о первой точке контакта для заказа|
  | ids | object | Идентификаторы заказа, включая `mindboxId` и `greenWaveOrderID` |
  | totalPrice | number | Общая стоимость заказа |
  | lines | array | Линии заказа |
  | appliedPromotions | array | Примененные акции к заказу |
  | area | object | Информация о зоне доставки |
  | deliveryCost| number | Стоимость доставки  |
  | payments | array | Информация об оплате заказа |
  | customFields | object | Пользовательские поля для заказа |
  | isCurrentState| boolean | Флаг, указывающий на текущее состояние заказа |

Информация о полях объекта `firstPointOfContact`:

```json
{
    ids: {
      mindboxId: number;
      externalId: string;
    };
    name: string;
  };
```

Информация о полях объекта `ids`:

```json
{
    mindboxId: number;
    websiteID: string;
    websiteID4fresh: string;
    greenWaveOrderID: string;
}
```

Информация о полях массива объектов `lines`:

```json
{
    product: {
      ids: {
        mindboxId: number;
        bitrix: string;
        expressDelivery: string;
        greenWave: string;
        regularDelivery: string;
        website: string;
      };
      name: string;
      description: string;
      price: number;
      pictureUrl: string;
    };
    quantity: number;
    quantityType: 'int' | 'double';
    basePricePerItem: number;
    priceOfLine: number;
    status: {
      ids: {
        externalId: string;
      };
    };
    appliedPromotions: {
      type:
        | 'earnedBonusPoints'
        | 'spentBonusPoints'
        | 'discount'
        | 'deliveryDiscount'
        | 'message'
        | 'preconditionMarker'
        | 'issuedCoupon';
      coupon?: {
        ids: {
          code: string;
        };
        pool: {
          ids: {
            mindboxId: number;
            externalId: string;
          };
          name: string;
          description: string;
        };
      };
      promotion: {
        ids: {
          mindboxId: number;
          externalId: string;
        };
        name: string;
        type: string;
      };
      limits?: {
        type: string;
        amount: {
          type: string;
          value: number;
        };
        used: {
          usageServiceStatus: string;
          amount: number;
        };
        untilDateTimeUtc: string;
      }[];
      groupingKey?: string;
      balanceType?: {
        ids: {
          systemName: string;
        };
        name: string;
      };
      amount: number;
      expirationDateTimeUtc?: string;
    }[];
    giftCard: {
      product: {
        ids: {
          mindboxId: number;
          bitrix: string;
          expressDelivery: string;
          greenWave: string;
          regularDelivery: string;
          website: string;
        };
        sku: {
          ids: {
            mindboxId: number;
            bitrix: string;
            expressDelivery: string;
            greenWave: string;
            regularDelivery: string;
            website: string;
          };
        };
      };
      amount: number;
      ids: {
        number: string;
      };
      status: {
        ids: {
          systemName: string;
        };
      };
      basePricePerItem: number;
    };
    lineNumber: string;
    lineId: string;
    customFields: {
      giftcardcallcenter: string;
      greenWavePromocode: string;
      rePaid: string;
    };
}
```

Информация о полях массива объектов `appliedPromotions`:

```json
{
    type: string;
    coupon: {
      ids: {
        code: string;
      };
      pool: {
        ids: {
          mindboxId: number;
          externalId: string;
        };
        name: string;
        description: string;
      };
    };
    promotion: {
      ids: {
        mindboxId: number;
        externalId: string;
      };
      name: string;
      type: string;
    };
    limits: {
      type: string;
      amount: {
        type: string;
        value: number;
      };
      used: {
        usageServiceStatus: string;
        amount: number;
      };
      untilDateTimeUtc: string;
    }[];
    groupingKey: string;
    balanceType: {
      ids: {
        systemName: string;
      };
      name: string;
    };
    amount: number;
    expirationDateTimeUtc: string;
}
```

Информация о полях объекта `area`:

```json
{
    ids: {
      externalId: string;
    };
}
```

Информация о полях массива объекта `payments`:

```json
{
    type: string;
    id: string;
    amount: number;
    promoActionId: string;
    creditCard: {
      hash: string;
    };
    balanceType: {
      ids: {
        systemName: string;
      };
      name: string;
    };
}
```

Информация о полях объекта `customFields`:

```json
{
    deliveryAddress: string;
    deliveryType: string;
    greenWaveTypeOrder: string;
    orderWareHouseId: string;
    preferredDeliveryTime4Fresh: string;
    replastic: string;
    reTicketUrl: string;
    zero: string;
    zero4Fresh: boolean;
}
```


2. **Рассчитать сумму корзины**

*Route:*
CALCULATE_CART ('v1/orders/calculate-auth-cart')

*Входные данные:*

    | Параметр | Тип данных | Валидация | Описание |
    | --- | --- | --- | --- |
    | userMindboxId | string | Обязательный | id пользователя в MindBox |
    | userPhoneNumber | string | Опциональный | Номер телефона пользователя |
    | productsItems | ProductItemDTO[] | Обязательный | Список продуктов |
    | promotions | string[] | Опциональный | Список акций |
    | deliveryCost | number | Обязательный, мин. знач. - 0 | Цена доставки |
    | debitCoins | number | Опциональный | Монеты |
    | debitRewards | number | Опциональный | Rewards |
    | paymentType | 'CARD' || 'CASH' | Опциональный, Enum | Тип оплаты |

ProductItemDTO:

    | Параметр | Тип данных | Валидация | Описание |
    | --- | --- | --- | --- |
    | productOldId | string | Обязательный | |
    | quantity | number | Обязательный | Количество продуктов |
    | basePrice | number | Обязательный | Начальная цена |
    | minPrice | number | Опциональный | Минимальная цена |
    | status | string | Обязательный | Статус |


*Функционал:*
Данный метод предназначен для рассчета стоимости товаров, находящихся в корзине.
Для расчета стоимости корзины вызывается defaultCalculateCart. 
Данный метод выполняет основные расчеты, используя переданные входные данные.
Далее происходит формирование списков с примененными и непримененными промокодами и скидками.
Далее происходит получение списка скидок по программе лояльности, подарочных сертификатов,


*Выходные данные:*
```json
{
  coins: number | null;
  rewards: number | null;
  orderTotalPrice: number;
  cashback: number;
  discountInfo: IDiscountInfo[];
  notAppliedPromotions: INotAppliedPromotion[];
  appliedPromotions: ICartAppliedPromotion[];
  productOffers: IProductOffer[];
  orderPresentArticles: string[];
  promotionPresentArticles: string[];
  couponPresents: ICouponPresent[];
  journalArticles: string[];
}
```

INotAppliedPromotion:
```json
{
  title: string;
  type: PromotionsType;
  status?: Status;
}
```

IDiscountInfo:
```json
{
  name: string;
  value: number;
  type: PromotionsType {
    {
    CERTIFICATE = 'CERTIFICATE',
    COUPON = 'COUPON',
    REFERRAL_CODE = 'REFFERAL_CODE',
    BASE = 'BASE',
    BONUS = 'BONUS',
    REWARDS = 'REWARDS',
    PRESENT = 'PRESENT',
    BY_CONDITION = 'BY_CONDITION',
  }
  };
}
```

ICartAppliedPromotion:
```json
 {
  title: string;
  description: string;
  type: PromotionsType;
  sum?: number;
  count?: number;
}
```

IProductOffer: 
```json
{
  article: string;
  discountInfo: IDiscountInfo[];
  cashback: number;
  sumWithDiscount: number;
  finalSellPrice: number;
}
```

ICouponPresent:
```json
{
  article: string;
  coupon: string;
}
```


3. **Изменение статуса линии заказа**

*Route:*
CHANGE_PRODUCTS_STATUS ('v1/orders/change-products-status')


*Входные данные:*

    | Параметр | Тип данных | Валидация | Описание |
    | --- | --- | --- | --- |
    | deviceUuid | string | Опциональный | id устройства |
    | websiteID4fresh | string | Обязательный | id на сайте 4fresh |
    | lines | LineStatusDTO[] | Обязательный | Линия заказа |

LineStatusDTO:

    | Параметр | Тип данных | Валидация | Описание |
    | --- | --- | --- | --- |
    | lineId | string | Обязательный | id линии заказа |
    | status | string | Обязательный | Статус позиции заказа |

*Функционал:*
Для изменения статуса в заказе у конкретной линии, необходимо вызвать метод `Website.ChangeLineStatus`. 
В запросе необходимо передавать только те линии, для которых необходимо изменить статус.

*Выходные данные:*
Возвращает объект со следующими полями:
```json
{
  order: {
    ids: {
      mindboxId: number;
      websiteID: string;
      websiteID4fresh: string;
      greenWaveOrderID: string;
    };
    customFields: {
      deliveryAddress: string;
      deliveryType: string;
      greenWaveTypeOrder: string;
      orderWareHouseId: string;
      preferredDeliveryTime4Fresh: string;
      replastic: string;
      reTicketUrl: string;
      zero: boolean;
      zero4Fresh: string;
    };
    returnedPayments: {
      type:
        | 'giftCard'
        | 'UponReceipt'
        | 'ByBankCard'
        | '1'
        | '9'
        | '11'
        | 'UMoney'
        | 'Qiwi'
        | 'BankCard'
        | '2'
        | '16'
        | '21'
        | '19'
        | '7'
        | '14'
        | '20'
        | '4'
        | '3'
        | '18'
        | '6';
      id: string;
      amount: number;
    };
    email: string;
    mobilePhone: number;
  };
  executionDateTimeUtc: string;
}
```

4. **Создание заказа**

*Route:*
CREATE ('v1/orders/create')

*Входные данные:*

    | Параметр | Тип данных | Валидация | Описание |
    | --- | --- | --- | --- |
    | deviceUuid | string | Опциональный | id устройства |
    | userPhoneNumber | string | Опциональный | Номер телефона пользователя |
    | userMindboxId | string | Обязательный | id пользователя в Mindbox |
    | orderNumber | string | Обязательный | Номер заказа |
    | productsItems | ProductItemDTO[] | Обязательный | Список продуктов |
    | promotions | string[] | Опциональный | Список акций |
    | deliveryCost | number | Обязательный, мин. знач. - 0 | Цена доставки |
    | debitCoins | number | Опциональный | Монеты |
    | debitRewards | number | Опциональный | Rewards |
    | paymentType | 'CARD' || 'CASH' | Опциональный, Enum | Тип оплаты |


*Функционал:*
Происходит создание заказа.
При нажатии на кнопку "Оформить заказ" вызывается операция `Website.BeginAuthorizedOrderTransaction`, которая блокирует баллы, промокоды, подарочные карты и фиксирует скидки по текущим акциям.
Если с момента вызова `Website.CalculateAuthorizedCart` цена заказа изменилась (например, акция закончилась), метод вернет статус `PriceHasBeenChanged.` 
В этом случае необходимо отобразить пользователю ошибку и заново рассчитать скидки с помощью операции `Website.CalculateAuthorizedCart`. 
При получении успешного ответа, сайт сохраняет заказ в свою базу данных и при успешном результате асинхронно вызывает операцию `Website.CommitOrderTransaction`.
В случае ошибки сайт должен отменить транзакцию с помощью операции `Website.RollbackOrderTransaction`.
При возникновении ошибок при создании заказа выбрасывает исключение `InternalServerErrorException`.


*Выходные данные:*
Объект со следующими полями:
```json
{
    balances: {
    total: number;
    available: number;
    blocked: number;
    nearestExpiration?: {
      total: number;
      date: string;
    };
    systemName: string;
    balanceType: {
      ids: {
        systemName: string;
      };
      name: string;
    };
  }[];
  order: {
    processingStatus: string;
    ids: {
      mindboxId: number;
    };
    transaction: {
      ids: {
        externalId: string;
      };
    };
    bonusPointsChanges: {
      balanceType: {
        ids: {
          systemName: string;
        };
        name: string;
      };
      earnedAmount: number;
      spentAmount: number;
    }[];
  };
}
```

5. **Изменение общего статуса заказа**

*Route:*
CHANGE_STATUS ('v1/orders/change-status')

*Входные данные:*

    | Параметр | Тип данных | Валидация | Описание |
    | --- | --- | --- | --- |
    | websiteID4fresh | string | Обязательный | id на сайте 4fresh |
    | deviceUuid | string | Опциональный | id устройства |
    | status | OrderStatusEnum | Обязательный, Enum | Статус заказа |

Статусы заказа:
```json
{
  IN_PROCESS = 'IN_PROCESS',
  NEW = 'NEW',
  WAIT = 'WAIT',
  PROCESSED = 'PROCESSED',
  COLLECT = 'COLLECT',
  COLLECTED = 'COLLECTED',
  READY_FOR_SHIPPING = 'READY_FOR_SHIPPING',
  SHIPPED = 'SHIPPED',
  SENDED = 'SENDED',
  ARRIVED = 'ARRIVED',
  RECEIVED = 'RECEIVED',
  PARTIALLY_RETURNED = 'PARTIALLY_RETURNED',
  DELIVERED = 'DELIVERED',
  RETURNED = 'RETURNED',
  CANCELLED = 'CANCELLED',
  LOST = 'LOST',
  UNDEFINED = 'UNDEFINED',
}
```

*Функционал:*
Для изменения общего статуса заказа вызывается метод `Website.UpdateOrderStatus` сервиса Mindbox.
Передается значение статуса Mindbox. Значение передается в соответствии с переданным в запросе поле статус.
Возвращает обновленный статус заказа.


*Выходные данные:*
Возвращает объект со следующими полями:
```json
{
  orderLinesStatus: string;
  order: {
    ids: {
      mindboxId: number;
      websiteID: string;
      websiteID4fresh: string;
      greenWaveOrderID: string;
    };
    customFields: {
      deliveryAddress: string;
      deliveryType: string;
      greenWaveTypeOrder: string;
      orderWareHouseId: string;
      preferredDeliveryTime4Fresh: string;
      replastic: string;
      reTicketUrl: string;
      zero: boolean;
      zero4Fresh: string;
    };
    email: string;
    mobilePhone: number;
  };
  executionDateTimeUtc: string;
}
```