---
title: Kurzlebige Datenschutzanbieter in ASP.NET Core
author: rick-anderson
description: Erfahren Sie Details zur Implementierung von ASP.NET Core kurzlebige-Datenschutzanbieter.
ms.author: riande
ms.date: 10/14/2016
uid: security/data-protection/implementation/key-storage-ephemeral
ms.openlocfilehash: e4b0014ab3bdbf90b91383e8a33102f94faa8153
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040567"
---
# <a name="ephemeral-data-protection-providers-in-aspnet-core"></a><span data-ttu-id="54ec8-103">Kurzlebige Datenschutzanbieter in ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="54ec8-103">Ephemeral data protection providers in ASP.NET Core</span></span>

<a name="data-protection-implementation-key-storage-ephemeral"></a>

<span data-ttu-id="54ec8-104">Es gibt Szenarien, in denen eine Anwendung einen Weg werfen erfordert `IDataProtectionProvider`.</span><span class="sxs-lookup"><span data-stu-id="54ec8-104">There are scenarios where an application needs a throwaway `IDataProtectionProvider`.</span></span> <span data-ttu-id="54ec8-105">Z. B. der Entwickler möglicherweise nur in einer Konsolenanwendung für die einmalige experimentiert werden, oder die Anwendung selbst ist flüchtig (es wird ein Skript erstellt oder ein Komponententestprojekt).</span><span class="sxs-lookup"><span data-stu-id="54ec8-105">For example, the developer might just be experimenting in a one-off console application, or the application itself is transient (it's scripted or a unit test project).</span></span> <span data-ttu-id="54ec8-106">Zur Unterstützung dieser Szenarios die [Microsoft.AspNetCore.DataProtection](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection/) Paket enthält einen Typ `EphemeralDataProtectionProvider`.</span><span class="sxs-lookup"><span data-stu-id="54ec8-106">To support these scenarios the [Microsoft.AspNetCore.DataProtection](https://www.nuget.org/packages/Microsoft.AspNetCore.DataProtection/) package includes a type `EphemeralDataProtectionProvider`.</span></span> <span data-ttu-id="54ec8-107">Dieser Typ stellt eine grundlegende Implementierung der `IDataProtectionProvider` , dessen Schlüssel Repository ist ausschließlich im Arbeitsspeicher gehalten und ist nicht in einen Sicherungsspeicher geschrieben.</span><span class="sxs-lookup"><span data-stu-id="54ec8-107">This type provides a basic implementation of `IDataProtectionProvider` whose key repository is held solely in-memory and isn't written out to any backing store.</span></span>

<span data-ttu-id="54ec8-108">Jede Instanz des `EphemeralDataProtectionProvider` verwendet einen eigenen eindeutigen Hauptschlüssel.</span><span class="sxs-lookup"><span data-stu-id="54ec8-108">Each instance of `EphemeralDataProtectionProvider` uses its own unique master key.</span></span> <span data-ttu-id="54ec8-109">Aus diesem Grund Wenn ein `IDataProtector` am Stamm einer `EphemeralDataProtectionProvider` generiert eine geschützte Nutzlast, diese Nutzlast kann nur durch ein entsprechendes ungeschützt sein `IDataProtector` (erhält die gleiche [Zweck](xref:security/data-protection/consumer-apis/purpose-strings#data-protection-consumer-apis-purposes) Kette) zur gleichen Stamm `EphemeralDataProtectionProvider` -Instanz.</span><span class="sxs-lookup"><span data-stu-id="54ec8-109">Therefore, if an `IDataProtector` rooted at an `EphemeralDataProtectionProvider` generates a protected payload, that payload can only be unprotected by an equivalent `IDataProtector` (given the same [purpose](xref:security/data-protection/consumer-apis/purpose-strings#data-protection-consumer-apis-purposes) chain) rooted at the same `EphemeralDataProtectionProvider` instance.</span></span>

<span data-ttu-id="54ec8-110">Das folgende Beispiel veranschaulicht die Instanziierung einer `EphemeralDataProtectionProvider` und zum Schützen und Aufheben des Schutzes von Daten.</span><span class="sxs-lookup"><span data-stu-id="54ec8-110">The following sample demonstrates instantiating an `EphemeralDataProtectionProvider` and using it to protect and unprotect data.</span></span>

```csharp
using System;
using Microsoft.AspNetCore.DataProtection;

public class Program
{
    public static void Main(string[] args)
    {
        const string purpose = "Ephemeral.App.v1";

        // create an ephemeral provider and demonstrate that it can round-trip a payload
        var provider = new EphemeralDataProtectionProvider();
        var protector = provider.CreateProtector(purpose);
        Console.Write("Enter input: ");
        string input = Console.ReadLine();

        // protect the payload
        string protectedPayload = protector.Protect(input);
        Console.WriteLine($"Protect returned: {protectedPayload}");

        // unprotect the payload
        string unprotectedPayload = protector.Unprotect(protectedPayload);
        Console.WriteLine($"Unprotect returned: {unprotectedPayload}");

        // if I create a new ephemeral provider, it won't be able to unprotect existing
        // payloads, even if I specify the same purpose
        provider = new EphemeralDataProtectionProvider();
        protector = provider.CreateProtector(purpose);
        unprotectedPayload = protector.Unprotect(protectedPayload); // THROWS
    }
}

/*
* SAMPLE OUTPUT
*
* Enter input: Hello!
* Protect returned: CfDJ8AAAAAAAAAAAAAAAAAAAAA...uGoxWLjGKtm1SkNACQ
* Unprotect returned: Hello!
* << throws CryptographicException >>
*/
```
