# GitTest
test git
<pre>
<code>
#ifndef __TEST_H__
#define __TEST_H__

#include "AXP/cplusplus/xplatform/include/type.h"
#include "AXP/cplusplus/xplatform/include/nullable.h"
#include "AXP/cplusplus/xplatform/include/astring.h"
#include "AXP/cplusplus/xplatform/include/list.h"
#include "AXP/cplusplus/xplatform/include/Parcel.h"
#include "AXP/cplusplus/xplatform/include/parcelable.h"
#include "AXP/cplusplus/libc/include/Common/ClassLoader.h"

namespace NA
{
    class CBase : public AXP::IParcelable, public AXP::CObject
    {
    public:

        AXP::ARESULT WriteToParcel(IN CONST AXP::Sp<AXP::CParcel> & parcel)
        {
            if (parcel == NULL)
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->WriteString(AXP::String::Create(L"NA.CBase"))))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->WriteByte(mB)))
                return AXP::AE_FAIL;

            return AXP::AS_OK;
        }

        AXP::ARESULT ReadFromParcel(IN CONST AXP::Sp<AXP::CParcel> & parcel)
        {
            if (parcel == NULL)
                return AXP::AE_FAIL;

            AXP::Sp<AXP::String> className;
            if (AXP::AFAILED(parcel->ReadString(className)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->ReadByte(mB)))
                return AXP::AE_FAIL;

            return AXP::AS_OK;
        }

        VIRTUAL AXP::Sp<AXP::String> ToString()
        {
            return AXP::String::Create(16, L"%d", mB);
        }

        VIRTUAL AXP::Sp<AXP::String> GetTypeName()
        {
            return AXP::String::Create(L"NA.CBase");
        }

    public:

        STATIC AXP::Sp<AXP::CObject> Create()
        {
            return new CBase();
        }

    public:

        AXP::Int8 mB;
    };

    class CList : public CBase
    {
    public:

        AXP::ARESULT WriteToParcel(IN CONST AXP::Sp<AXP::CParcel> & parcel)
        {
            if (parcel == NULL)
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->WriteString(AXP::String::Create(L"NA.CList"))))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(CBase::WriteToParcel(parcel)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->WriteInt8(a)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->WriteInt16(b)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->WriteInt64(c)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->WriteDouble(e)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->WriteBoolean(bee)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->WriteNullableInt8(f)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->WriteNullableInt64(g)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->WriteString(m)))
                return AXP::AE_FAIL;

            {
                AXP::Int32 length;
                if (lstring == NULL)
                    length = 0;
                else
                    length = lstring->GetCount();

                AXP::Int8 type = 'L';
                if (AXP::AFAILED(parcel->Write((AXP::PCByte)&type, sizeof(type))))
                    return AXP::AE_FAIL;

                if (AXP::AFAILED(parcel->Write((AXP::PCByte)&length, sizeof(length))))
                    return AXP::AE_FAIL;

                if (lstring) {
                    Foreach(AXP::String, obj, lstring) {
                        if (obj == NULL)
                            return AXP::AE_FAIL;

                        if (AXP::AFAILED(parcel->WriteString(obj)))
                            return AXP::AE_FAIL;
                    }
                }
            }

            {
                AXP::Int32 length;
                if (list64 == NULL)
                    length = 0;
                else
                    length = list64->GetCount();

                AXP::Int8 type = 'L';
                if (AXP::AFAILED(parcel->Write((AXP::PCByte)&type, sizeof(type))))
                    return AXP::AE_FAIL;

                if (AXP::AFAILED(parcel->Write((AXP::PCByte)&length, sizeof(length))))
                    return AXP::AE_FAIL;

                if (list64) {
                    Foreach(AXP::Int64$, obj, list64) {
                        if (obj == NULL)
                            return AXP::AE_FAIL;

                        if (AXP::AFAILED(parcel->WriteNullableInt64(obj->GetValue())))
                            return AXP::AE_FAIL;
                    }
                }
            }

            {
                AXP::Int32 length;
                if (listDouble == NULL)
                    length = 0;
                else
                    length = listDouble->GetCount();

                AXP::Int8 type = 'L';
                if (AXP::AFAILED(parcel->Write((AXP::PCByte)&type, sizeof(type))))
                    return AXP::AE_FAIL;

                if (AXP::AFAILED(parcel->Write((AXP::PCByte)&length, sizeof(length))))
                    return AXP::AE_FAIL;

                if (listDouble) {
                    Foreach(AXP::Double$, obj, listDouble) {
                        if (obj == NULL)
                            return AXP::AE_FAIL;

                        if (AXP::AFAILED(parcel->WriteNullableDouble(obj->GetValue())))
                            return AXP::AE_FAIL;
                    }
                }
            }

            return AXP::AS_OK;
        }

        AXP::ARESULT ReadFromParcel(IN CONST AXP::Sp<AXP::CParcel> & parcel)
        {
            if (parcel == NULL)
                return AXP::AE_FAIL;

            AXP::Sp<AXP::String> className;
            if (AXP::AFAILED(parcel->ReadString(className)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(CBase::ReadFromParcel(parcel)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->ReadInt8(a)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->ReadInt16(b)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->ReadInt64(c)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->ReadDouble(e)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->ReadBoolean(bee)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->ReadNullableInt8(f)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->ReadNullableInt64(g)))
                return AXP::AE_FAIL;

            if (AXP::AFAILED(parcel->ReadString(m)))
                return AXP::AE_FAIL;

            {
                AXP::Int8 type;
                if (AXP::AFAILED(parcel->Read((AXP::PByte)&type, sizeof(type), sizeof(type))))
                    return AXP::AE_FAIL;

                if (type != 'L')
                    return AXP::AE_FAIL;

                AXP::Int32 length;
                if (AXP::AFAILED(parcel->Read((AXP::PByte)&length, sizeof(length), sizeof(length))))
                    return AXP::AE_FAIL;

                lstring = new AXP::List<AXP::String>();
                if (lstring == NULL)
                    return AXP::AE_FAIL;

                for (AXP::Int32 i = 0; i < length; i++) {
                    AXP::Sp<AXP::String> obj;
                    if (AXP::AFAILED(parcel->ReadString(obj)))
                        return AXP::AE_FAIL;

                    if (!lstring->PushBack(obj))
                        return AXP::AE_FAIL;
                }
            }

            {
                AXP::Int8 type;
                if (AXP::AFAILED(parcel->Read((AXP::PByte)&type, sizeof(type), sizeof(type))))
                    return AXP::AE_FAIL;

                if (type != 'L')
                    return AXP::AE_FAIL;

                AXP::Int32 length;
                if (AXP::AFAILED(parcel->Read((AXP::PByte)&length, sizeof(length), sizeof(length))))
                    return AXP::AE_FAIL;

                list64 = new AXP::List<AXP::Int64$>();
                if (list64 == NULL)
                    return AXP::AE_FAIL;

                for (AXP::Int32 i = 0; i < length; i++) {
                    AXP::Int64$ obj;
                    if (AXP::AFAILED(parcel->ReadNullableInt64(obj)))
                        return AXP::AE_FAIL;

                    if (!list64->PushBack(new AXP::Int64$(obj)))
                        return AXP::AE_FAIL;
                }
            }

            {
                AXP::Int8 type;
                if (AXP::AFAILED(parcel->Read((AXP::PByte)&type, sizeof(type), sizeof(type))))
                    return AXP::AE_FAIL;

                if (type != 'L')
                    return AXP::AE_FAIL;

                AXP::Int32 length;
                if (AXP::AFAILED(parcel->Read((AXP::PByte)&length, sizeof(length), sizeof(length))))
                    return AXP::AE_FAIL;

                listDouble = new AXP::List<AXP::Double$>();
                if (listDouble == NULL)
                    return AXP::AE_FAIL;

                for (AXP::Int32 i = 0; i < length; i++) {
                    AXP::Double$ obj;
                    if (AXP::AFAILED(parcel->ReadNullableDouble(obj)))
                        return AXP::AE_FAIL;

                    if (!listDouble->PushBack(new AXP::Double$(obj)))
                        return AXP::AE_FAIL;
                }
            }

            return AXP::AS_OK;
        }

        VIRTUAL AXP::Sp<AXP::String> ToString()
        {
            AXP::Sp<AXP::String> json = AXP::String::Create(L"{");
            if (json == NULL)
                return NULL;

            json = AXP::String::Create(json->Length() + 47, L"%ls\"a\":\"%d\",", (AXP::PCWStr)*json, a);
            if (json == NULL)
                return NULL;

            json = AXP::String::Create(json->Length() + 47, L"%ls\"b\":\"%d\",", (AXP::PCWStr)*json, b);
            if (json == NULL)
                return NULL;

            json = AXP::String::Create(json->Length() + 47, L"%ls\"c\":\"%lld\",", (AXP::PCWStr)*json, c);
            if (json == NULL)
                return NULL;

            json = AXP::String::Create(json->Length() + 315, L"%ls\"e\":\"%.2f\",", (AXP::PCWStr)*json, e);
            if (json == NULL)
                return NULL;

            json = AXP::String::Create(json->Length() + 47, L"%ls\"bee\":\"%ls\",", (AXP::PCWStr)*json, bee ? L"true" : L"false");
            if (json == NULL)
                return NULL;

            if (!f.HasValue()) {
                json = AXP::String::Create(json->Length() + 40, L"%ls\"f\":\"\",", (AXP::PCWStr)*json);
                if (json == NULL)
                    return NULL;
            }
            else {
                json = AXP::String::Create(json->Length() + 64, L"%ls\"f\":\"%d\",", (AXP::PCWStr)*json, f.GetValue());
                if (json == NULL)
                    return NULL;
            }

            if (!g.HasValue()) {
                json = AXP::String::Create(json->Length() + 40, L"%ls\"g\":\"\",", (AXP::PCWStr)*json);
                if (json == NULL)
                    return NULL;
            }
            else {
                json = AXP::String::Create(json->Length() + 64, L"%ls\"g\":\"%lld\",", (AXP::PCWStr)*json, g.GetValue());
                if (json == NULL)
                    return NULL;
            }

            if (m == NULL) {
                json = AXP::String::Create(json->Length() + 40, L"%ls\"m\":\"\",", (AXP::PCWStr)*json);
                if (json == NULL)
                    return NULL;
            }
            else {
                json = AXP::String::Create(json->Length() + m->Length() + 40, L"%ls\"m\":\"%ls\",", (AXP::PCWStr)*json, (AXP::PCWStr)*m);
                if (json == NULL)
                    return NULL;
            }

            if (lstring == NULL) {
                json = AXP::String::Create(json->Length() + 40, L"%ls\"lstring\":[],", (AXP::PCWStr)*json);
                if (json == NULL)
                    return NULL;
            }
            else {
                AXP::Sp<AXP::String> jsonTmp = AXP::String::Create(L"\"lstring\":[");
                if (jsonTmp == NULL)
                    return NULL;

                for(AXP::Int32 i = 0; i < lstring->GetCount(); ++i) {
                    AXP::Sp<AXP::String> obj = (*lstring)[i];
                    AXP::PCWStr comma;
                    if (i < lstring->GetCount() - 1)
                        comma = L",";
                    else
                        comma = L"";

                    if (obj == NULL)
                        jsonTmp = AXP::String::Create(json->Length() + 39, L"%ls\"\"%ls", (AXP::PCWStr)*json, comma);
                    else
                        jsonTmp = AXP::String::Create(jsonTmp->Length() + obj->Length() + 39, L"%ls\"%ls\"%ls", (AXP::PCWStr)*jsonTmp, i, (AXP::PCWStr)*obj, comma);
                    if (jsonTmp == NULL)
                        return NULL;
                }

                jsonTmp = AXP::String::Create(jsonTmp->Length() + 7, L"%ls],", (AXP::PCWStr)*jsonTmp);
                if (jsonTmp == NULL)
                    return NULL;

                json = AXP::String::Create(json->Length() + jsonTmp->Length() + 2, L"%ls%ls", (AXP::PCWStr)*json, (AXP::PCWStr)*jsonTmp);
                if (json == NULL)
                    return NULL;
            }

            if (list64 == NULL) {
                json = AXP::String::Create(json->Length() + 40, L"%ls\"list64\":[],", (AXP::PCWStr)*json);
                if (json == NULL)
                    return NULL;
            }
            else {
                AXP::Sp<AXP::String> jsonTmp = AXP::String::Create(L"\"list64\":[");
                if (jsonTmp == NULL)
                    return NULL;

                for(AXP::Int32 i = 0; i < list64->GetCount(); ++i) {
                    AXP::Sp<AXP::Int64$> obj = (*list64)[i];
                    AXP::PCWStr comma;
                    if (i < list64->GetCount() - 1)
                        comma = L",";
                    else
                        comma = L"";

                    if ((obj == NULL) || (!obj->HasValue()))
                        jsonTmp = AXP::String::Create(jsonTmp->Length() + 47, L"%ls\"\"%ls", (AXP::PCWStr)*jsonTmp, comma);
                    else
                        jsonTmp = AXP::String::Create(jsonTmp->Length() + 47, L"%ls\"%lld\"%ls", (AXP::PCWStr)*jsonTmp, obj->GetValue(), comma);

                    if (jsonTmp == NULL)
                        return NULL;
                }

                jsonTmp = AXP::String::Create(jsonTmp->Length() + 7, L"%ls],", (AXP::PCWStr)*jsonTmp);
                if (jsonTmp == NULL)
                    return NULL;

                json = AXP::String::Create(json->Length() + jsonTmp->Length() + 2, L"%ls%ls", (AXP::PCWStr)*json, (AXP::PCWStr)*jsonTmp);
                if (json == NULL)
                    return NULL;
            }

            if (listDouble == NULL) {
                json = AXP::String::Create(json->Length() + 40, L"%ls\"listDouble\":[]", (AXP::PCWStr)*json);
                if (json == NULL)
                    return NULL;
            }
            else {
                AXP::Sp<AXP::String> jsonTmp = AXP::String::Create(L"\"listDouble\":[");
                if (jsonTmp == NULL)
                    return NULL;

                for(AXP::Int32 i = 0; i < listDouble->GetCount(); ++i) {
                    AXP::Sp<AXP::Double$> obj = (*listDouble)[i];
                    AXP::PCWStr comma;
                    if (i < listDouble->GetCount() - 1)
                        comma = L",";
                    else
                        comma = L"";

                    if ((obj == NULL) || (!obj->HasValue()))
                        jsonTmp = AXP::String::Create(jsonTmp->Length() + 47, L"%ls\"\"%ls", (AXP::PCWStr)*jsonTmp, obj->GetValue(), comma);
                    else
                        jsonTmp = AXP::String::Create(jsonTmp->Length() + 47, L"%ls\"%.2f\"%ls", (AXP::PCWStr)*jsonTmp, obj->GetValue(), comma);

                    if (jsonTmp == NULL)
                        return NULL;
                }

                jsonTmp = AXP::String::Create(jsonTmp->Length() + 7, L"%ls]", (AXP::PCWStr)*jsonTmp);
                if (jsonTmp == NULL)
                    return NULL;

                json = AXP::String::Create(json->Length() + jsonTmp->Length() + 2, L"%ls%ls", (AXP::PCWStr)*json, (AXP::PCWStr)*jsonTmp);
                if (json == NULL)
                    return NULL;
            }

            return AXP::String::Create(json->Length() + 7, L"%ls}", (AXP::PCWStr)*json);
        }

        VIRTUAL AXP::Sp<AXP::String> GetTypeName()
        {
            return AXP::String::Create(L"NA.CList");
        }

    public:

        STATIC AXP::Sp<AXP::CObject> Create()
        {
            return new CList();
        }

    public:

        AXP::Int8 a;
        AXP::Int16 b;
        AXP::Int64 c;
        AXP::Double e;
        AXP::Boolean bee;
        AXP::Int8$ f;
        AXP::Int64$ g;
        AXP::Sp<AXP::String> m;
        AXP::Sp<AXP::List<AXP::String > > lstring;
        AXP::Sp<AXP::List<AXP::Int64$ > > list64;
        AXP::Sp<AXP::List<AXP::Double$ > > listDouble;
    };

    STATIC AXP::Boolean _NA_CBase_ = AXP::Libc::Common::ClassLoader::RegisterClassCreator(L"NA.CBase", NA::CBase::Create);
    STATIC AXP::Boolean _NA_CList_ = AXP::Libc::Common::ClassLoader::RegisterClassCreator(L"NA.CList", NA::CList::Create);
}
#endif // __TEST_H__
</code>
</pre>
